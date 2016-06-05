---
layout:     post
title:      Dependencies and Robustness
date:       2016-06-06 01:06:00 +0200
author:     Robert Konrad
authorlink: http://robdangero.us
permalink:  dependencies-and-robustness
---
"why is haxelib not liked?" - this question comes up semi-regularly in regards to my software in lots of different variations. Full context: haxelib is the package manager of Haxe, which is a programming language I tend to use a lot. I put versions of my software on haxelib but I encourage users to only use that for experiments and migrate to the git version (which is structured a little differently) for real projects. And I indeed do not like haxelib. I also do not like npm or even apt. Because package managers are not robust. Do you remember the [recent npm tragedy](http://blog.npmjs.org/post/141577284765/kik-left-pad-and-npm)? That's just one of many ways in which package managers can fail.

Just imagine you build a product which is composed of some source code you wrote and some dependencies you linked in. But wait, that's really not what it's like. You build a product which is composed of some source code. It doesn't matter who wrote the source code. When you link in some extra code it becomes your responsibility because it ends up being part of your product. This includes the source code of most tools you use, especially your compilers. Because if any part of that fails, your product fails. Maybe you don't care and more often than not that's probably kind of ok. But sometimes you have to care. Maybe you're building a game, got some financing, signed some contracts - and you have to ship at a certain date or else contractual penalties will crush your company. Two weeks to go, you notice your game crashes in the last level. But didn't that work before? Hm, what version of GCC did we use for our previous tests? Good luck to you if you didn't version everything and have all source code available so you can apply a minimal fix.

The world of software is a world of bugs, compatibility problems and performance regressions. So far all attempts to fundamentally change this situation failed, so a package manager should allow your software to survive in this world. The requirements for that are pretty straight forward:

* All the source code, all the revisions, all the time.
* Easy replication of the whole thing.
* Fully versioned local fixes to all dependencies.

Any yet all of this seems to be low priority for package managers, if possible at all.

Versioning systems on the other hand tend to solve that. They usually provide some sort of dependency system. In git that's called submodules. Submodules are a little cumbersome to use, but at least they get the basics right. By default you get all revisions. The revision of every submodule is always recorded so local fixes are versioned. When you copy the directory tree, you get everything - you can then work offline or setup your own git server.

But more often than not software is now run in automatically updated web-browsers, so isn't robustness out the window anyway? Pretty much, but that's just one more reason to make your development process even more robust to counteract these developments. Nowadays basically at any time you might be forced to somehow fix your software so it keeps working in a constantly changing environment.

Personally I'm responsible for a software package called [Kha](http://kha.tech). I make compromises with Kha to keep download sizes somewhat reasonable. Tool/compiler submodules contain just the binaries, original revisions are recorded in the commits. I don't put in the C/C++ compilers because in many cases that isn't even legally possible, ...

Whatever you do, it likely won't be perfect due to external circumstances. But you can at least avoid using package managers - because package managers are based on the assumption that you can ignore the source code you depend on, but doing so is a recipe for disaster.
