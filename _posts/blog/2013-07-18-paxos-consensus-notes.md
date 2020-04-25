---
title: 'Paxos Consensus &#8211; Notes'
author: Ninad
layout: post
permalink: /blog/2013/07/paxos-consensus-notes/
categories:
  - Blog
  - Uncategorized
---
I came across this algorithm used for generating a consensus among distributed systems, recording the material I liked/groked among it all

  * The original [paper](http://www.cs.utexas.edu/users/lorenzo/corsi/cs380d/past/03F/notes/paxos-simple.pdf) by Leslie Lamport
  * The Wikipedia page, with some examples: [http://en.wikipedia.org/wiki/Paxos\_(computer\_science)][1]
  * A (blogpost](http://blog.aetherworks.com/2013/05/paxos-by-example/) - A comment on Reddit mentions that this might be the cleanest explanations around, and I agree.
  * Any list of links on Paxos cannot be complete without a reference to the FLP impossibility explained [here](http://the-paper-trail.org/blog/a-brief-tour-of-flp-impossibility) and the original paper is available [here](http://cs-www.cs.yale.edu/homes/arvind/cs425/doc/fischer.pdf)
  * A [blogpost](http://blog.willportnoy.com/2012/06/lessons-learned-from-paxos.html) that would make sense after I've slept over this algorithm a little, and tried implementing it. These are the experiences of implementing it for Windows Azure.
  * Yet another [paper](http://dl.acm.org/citation.cfm?id=1281103) that talks about an implementation, this time by Google

I'm still looking for an example of how this is done in databases though.

 [1]: http://en.wikipedia.org/wiki/Paxos_(computer_science)
