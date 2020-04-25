---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: page
---

# Ninad Pundalik

## Just another homepage

### About

I'm a Site Reliability Engineer with [Slack](http://slack.com), working in their India office. During the day, I do my best to keep you productive and happy at work. After work, I read, attend music concerts, find new places to eat, and drink lots of tea and coffee. Some people also say that I yap a lot. To contact me, DM me on Twitter: [@ni_nad](https://twitter.com/ni_nad "Ninad on Twitter")


### Posts

{% for post in site.posts %}

#### [{{ post.title }}]({{ post.url }})

_{{ post.date | date: "%B %e, %Y" }}_

{{ post.excerpt }}

{% endfor %}
