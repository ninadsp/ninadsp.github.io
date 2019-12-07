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

  * <span style="line-height: 13px;"><span style="line-height: 13px;">The original paper by Leslie Lamport: </span></span><http://www.cs.utexas.edu/users/lorenzo/corsi/cs380d/past/03F/notes/paxos-simple.pdf>
  * The Wikipedia page, with some examples: [http://en.wikipedia.org/wiki/Paxos\_(computer\_science)][1]
  * A blogpost: <http://blog.aetherworks.com/2013/05/paxos-by-example/> &#8211; A comment on Reddit mentions that this might be the cleanest explanations around, and I agree.
  * Any list of links on Paxos cannot be complete without a reference to the FLP impossibility explained at <http://the-paper-trail.org/blog/a-brief-tour-of-flp-impossibility/> and the original paper is available at <http://cs-www.cs.yale.edu/homes/arvind/cs425/doc/fischer.pdf>
  * A blogpost that would make sense after I've slept over this algorithm a little, and tried implementing it: <http://blog.willportnoy.com/2012/06/lessons-learned-from-paxos.html>. These are the experiences of implementing it for Windows Azure.
  * Yet another paper that talks about an implementation, this time by Google: <http://dl.acm.org/citation.cfm?id=1281103>

I'm still looking for an example of how this is done in databases though.

 [1]: http://en.wikipedia.org/wiki/Paxos_(computer_science)