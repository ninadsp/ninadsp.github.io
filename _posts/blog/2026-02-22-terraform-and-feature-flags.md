---
title: Terraform, Feature Flags and Configurability
author: Ninad
layout: post
permalink: /blog/2026/02/terraform-and-feature-flags/
tags:
  - terraform
  - feature flags
  - jsonet
  - configuration
categories:
  - Blog
---

[Terraform](https://developer.hashicorp.com/terraform) has been my bread and butter for the past few years as the tool for Infrastructure as Code. I've dealt with a variety of patterns while working with Terraform, and noticed one pattern that is rarely discussed, but super useful. [Feature flags](https://martinfowler.com/articles/feature-toggles.html) are a way to write code that can behave differently based on how we configure things, and is as old as writing code for computers. It gives the author of the code flexibility to have different implementations, safely migrate systems from one approach or capability to a new one and choose behaviour based on the target context. Mature codebases find tooling or affordances that give them the ability to evolve and adapt, and feature flags are one pattern to achieve that. However, the public internet has very few examples about how to achieve this for Infrastructure as Code tools, including Terraform.

The best place to start is HashiCorp's [official post](https://www.hashicorp.com/en/blog/terraform-feature-toggles-blue-green-deployments-canary-test) about feature flags. All resources support a few basic arguments, including `count`. The main example from this post use nos `count`, coupled with a boolean variable to toggle the existence of a resource. This is a super basic example though, and it only [shows](https://knowyourmeme.com/memes/how-to-draw-an-owl) how to draw the first two circles of an owl. How does one finish the drawing though? Let us work through some examples below to draw the rest of the owl.

```
# A basic example with count
locals {
    foo_enabled = true
    ...
}

resource "provider_bar_foo" "foo_thing" {
    count = local.foo_enabled ? 1 : 0
    ...
}
```

If you've been writing Terraform code for a while, then you're definitely using [modules](https://developer.hashicorp.com/terraform/language/modules/develop) to reduce repetition and to build reusable blocks. If you know what behaviors of the module need to be configurable, you can then define variables that enable or disable various resources. Due to their nature, booleans always limit us to off and on states. They don't give us a lot of flexibility in expressing our intent through the codebase. If the modules you're writing are meant for a wide and public distribution (like the [Cloud Posse project](https://github.com/orgs/cloudposse/repositories), or [Google Cloud's Terraform modules](https://github.com/orgs/terraform-google-modules/repositories)), it makes sense to follow this pattern of using boolean variables to manage features.

```
# An example of how some public modules have to be defined
locals {
    foo_enabled = true
    bar_enabled = false
    baz_enabled = false
    ...
}

module "services_group_1" {
    source = ".../path/to/module"
    region = "abc-def-01"
    foo_enabled = local.foo_enabled
    bar_enabled = local.bar_enabled
    baz_enabled = local.baz_enabled
}

module "services_group_2" {
    source = ".../path/to/module"
    region = "xyz-tuv-02"
    foo_enabled = local.foo_enabled
    bar_enabled = local.bar_enabled
    baz_enabled = local.baz_enabled
}
```

As you start writing modules with this approach, you realise that the conditionals start growing, and the right side of the `count` attribute starts becoming much more complex.

```
# A complex feature flag evaluation
locals {
    baz_enabled = true
    green_deployment = false
    blue_deployment = true
}

resource "provider_bar_baz" "baz_green" {
    count = (local.baz_enabled && local.green_deployment) ? 1 : 0 
}

resource "provider_bar_baz" "baz_blue" {
    count = (local.baz_enabled && local.blue_deployment) ? 1 : 0 
}
```

I've seen a great pattern that helps solve this complexity. You can write a Python or Golang script that can take a few parameters as an input, and emits a JSON object that can then be parsed by Terraform. This let's you express your conditionals in a language that is more readable, maintainable, and frankly, friendlier than HCL. Your Terraform also stays relatively simple. In a previous team, a member wrote a module that managed a barebones container hosting platform via Terraform, and any product team could use it to run an application. Naturally, the matrix of choices required to support an app, blue green deployments, databases, and other features together made the module fairly large. By writing a Go script that accepted some parameters and translated them into a detailed configuration, the member made the module approachable to other engineers in the organization, and also gained a good amount of flexibility in deploying applications. And, the great thing about this approach is: any language or binary that can render a JSON object is supported. If you really wanted, you could write a bash script that uses `jq`, or even a Perl script! (Although, I'd highly question your sanity if you wrote Perl for this)

```
#!/usr/bin/env python 3
# A sample Python script

import json
import sys

BASE_CONFIG = {
    "foo_enabled": True,
    "foo_a": "bar",
    ...
}
ENV_CONFIG = {
    "dev": {},
    "staging": {
        "foo_enabled": True,
    },
    "production": {
        "foo_enabled": False,
    },
}

# Super dumb implementation for illustration, needs more error handling
if __name__ == "__main__":
    query = json.load(sys.stdin)
    environment = query.get("environment")
    
    merged_config = { **BASE_CONFIG, **ENV_CONFIG[environment]}
    print(json.dumps(merged_config))
```

```
# How to consume in TF
data "external" "config" {
    program = ["python3", "path/to/generate_config.py"]
    
    query = {
        environment = "production"
    }
}

locals {
    cfg = data.external.config.result
}

resource "provider_bar_foo" "foo_thing" {
    count = local.cfg.foo_enabled ? 1 : 0
    parameter_a = local.cfg.foo_a
    ...
} 
```

However, if the Terraform you're writing is meant for internal usage only, we can exploit this path further and gain a lot more flexibility. Feature flags do not need to only have a boolean shape. They can be an integer (e.g. a count of resources, to setup 2 nodes in staging and 5 in production), a list of strings (a list of buckets to create in a region), or a more complex object (a full specification of the firewall rules associated with a particular set of nodes). And, Terraform supports all these types! This lets us define a simple module, and have it iterate on a list of objects. It is now easier to reason about how rollouts progress, and also makes the module less brittle.  By shifting the creation/modification of resources out of the module, and into a configuration layer, the module has suddenly become a lot more flexible.

```
# A more complex object used to create N copies of the same resource/module
locals {
    foo_names = {
        "abc": {},
        "def": {},
        "xyz": {}.
    }
}

module "foo" {
    source = "../path/to/foo"
    for_each = set(local.foo_names)
    
    name = each.key
}
```

My current team has taken this approach to the next logical step. Instead of generating a JSON file with a homebrew script that will, over time, become a fragile and unmaintainable mess, we've picked [jsonnet](jsonnet.org), a language that renders to JSON. Other formats like `ini`, `toml` and `yaml` are supported, but `json` is the primary target. Although slightly more limited in terms of language features, it has been designed explicitly as a configuration generator, making it well suited for this task. Create a base specification that describes what a region or cluster of services will look like, and use jsonnet to generate JSON configurations for each of them. You may choose to generate them at runtime by running the `jsonnet` command through Terraform, or you could check the generated configuration into your repo, either works. The moment you're dealing with more than 5 clusters (e.g. dev, staging, prod, and/or regions distributed across the globe to serve multiple customers), the generated configuration becomes an invaluable tool in your belt. From safely releasing features, to dealing with quirks of cloud providers and regions, everything can be expressed as a flag. And, most importantly, the barrier to introduce risky changes lowers by a lot. This also gives the team a pathway to manage many kinds of tech debt at a much lower level of risk.

Jsonnet also allows you to write tests (although, to me, the ergonomics of tests in jsonnet feel a little clunky), which ensures that regressions and misconfigurations can be caught early. We configure multiple node pools per kubernetes cluster, and generate all the attributes via jsonnet. We also support a limited number of OS images (due to compliance/security reasons), so we wrote a test that checks each node pool's OS image names, ensuring that match specific regex patterns. As this test is executed at build time, we can catch any errors (hey, we're humans and typos are normal!) when we raise a PR, rather than attempting a Terraform apply and have it bail on us.

Another neat thing that you can try at this stage is, instead of passing in individual values and booleans of the feature flags through each abstraction layer of your Terraform modules, you can just pass in the entire configuration JSON block to everything. This simplifies adding a new feature flag, as you only need to change your jsonnet specification, and the final piece of Terraform that consumes that code.

```
# base.libsonnet
base_env:: {
    foo: {
        enabled: false,
        bar: "baz",
        abc: "def",
    }
},

dev:: self.base + { enabled: true, },
prod:: self.base,
```

```
# environments.jsoonnet
local base = import 'base.libsonnet';

{
    dev: base.dev,
    prod: base.prod,
}
```

```
variable "environment" {
    type = "string"
}

locals {
    all_cfg = jsondecode(file("path/to/generated/environments.json"))
    cfg = local.all_cfg[var.environment]
}

resource "provider_bar_foo" "foo" {
    count = local.cfg.foo.enabled ? 1 : 0
    bar = local.cfg.foo.bar
    ...
}
```

```
jsonnet /path/to/environments.jsonnet
```

Some stuff to keep in mind when picking this path:

* If your team has a well defined versioning and distribution system for Terraform modules, the module can evolve with product needs. A configuration object will still be valuable, but it solves the module brittleness problem I talked about before.
* Using `count` to manage objects is known to cause state churn as your infrastructure evolves. Hence, more teams have started to favour `for_each` instead. If the complexity of the confiugration choices is still not very high, a well designed `for_each` object will get you most of the benefits of feature flags and generated configuration without the additional overhead of having a pre-commit step to generate the JSON files.
* If you're using an external script to generate configurations during each terraform plan/apply stage, you need to guarantee a stable execution environment for your chosen language. The same Python or Golang version needs to exist on your engineer's machine, as well as the machines used to do your terraform applies (i.e. the Github Actions runners, or Terraform Cloud VMs).
* By sending the entire configuration object through various layers of Terraform modules, you do end up trading some level of strictness (which you would have if you validated every variable for type and structure at every abstraction layer) for speed, but it might be a trade off that makes sense to you.
* If you're developing Terraform for target contexts that end up varying a lot from each other, and/or require enabling/disabling entire modules, this approach can be more clunky. Consider languages/frameworks like Pulumi and Terragrunt instead that give you more expressivity than HCL.

Have I convinced you enough to experiment with feature flags for the next major Terraform change? If you've seen any other interesting, or similarly effective ways to manage Infrastructure as Code tools and codebases, ping me on Mastodon, I'd love to hear about them and learn from you!

Additional reading:

* [https://adhoc.team/2019/09/24/feature-flags-dynamic-blocks-terraform/](https://adhoc.team/2019/09/24/feature-flags-dynamic-blocks-terraform/)
* [https://medium.com/@leslie.alldridge/terraform-external-data-source-using-custom-python-script-with-example-cea5e618d83e](https://medium.com/@leslie.alldridge/terraform-external-data-source-using-custom-python-script-with-example-cea5e618d83e)