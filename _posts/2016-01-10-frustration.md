---
layout:     post
title:      Snippets of Frustration
date:       2016-01-10 18:21:00 +0200
author:     Robert Konrad
authorlink: http://robdangero.us
permalink:  frustration
---
When implementing system code like in Kha's and Kore's system backends every now and then one comes across something really silly. The supposedly simplest things in the world can take days of work because some companies seem to have no interest at all in making sure simple things stay simple (after all one can always use their higher level libraries which have the added benefit of much more effective vendor lock-in).
The *Snippets of Frustration* document those moments of frustration. They are basically small snippets of code for really simple stuff that nonetheless took a long time to put together. They are here to give a better understanding of the internals of Kha and Kore - it's the magic sauce that makes them run smoothly everywhere. But the series is also especially useful for people who decide not to use Kha or Kore; because we have to face it - those people do exist... at least for now.
The series is also supposed to provide the necessary impulse to instigate detailed discussions about those methods. You might know of a better implementation for a particular snippet. If that is the case, please don't go away. Please leave a comment to help all of us to make our code more robust.

1. [Own the Main Loop in iOS](http://kode.tech/snippet-1-own-the-main-loop-in-ios)
