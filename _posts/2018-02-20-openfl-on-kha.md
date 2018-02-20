---
layout:     post
title:      A Pitch for OpenFL on Kha
date:       2018-02-20 06:36:00 +0200
author:     Robert Konrad
authorlink: http://robdangero.us
permalink:  openfl-on-kha
---
So, this is where we're at - I got the most basic OpenFL sample running by putting a Kha backend in lime and a Kha renderer in OpenFL and I think I have a good understanding of what to do to make everything else run. But should I really do this? People trying to talk me into making Kha more like Flash is one of the more unpleasant parts of the whole affair. I get my kicks from seeing people learn about modern GPU programming via Kha so intrinsic motivation for providing Flash-like functionality is severely lacking. But making OpenFL run on Kha is something that comes up again and again and solving all flashy Kha demands like that makes sense and is not crazy difficult. Nonetheless I failed again and again to motivate anybody to actually do it so by now I'm pretty sure it won't happen unless I do it myself. I am a greedy bastard though so here are my demands: I want a black Super Nt delivered to my door step - because there's no better way to boost motivation than building connotations to SNES games. When I work on OpenFL I want to think of Super Mario Kart. Make that happen and you will be able to run all your HaxeFlixel games and more on Kha by this year’s Haxe Summit. Shy away from it and I have a nicely absurd reason to point my finger at whenever I dismiss OpenFL requests in the future.

Undecided on whether to help out with that? Let me help you out with all the pros and cons of OpenFL on Kha I could think of:

### Pros:
* True cross-platform support. No reliance on OpenGL or SDL or anything else which might or might not work reliably and efficiently in the future. GPU API access is abstracted, shaders are cross-compiled - this runs natively on all moderately modern hardware using the fastest and most robust platform APIs available on each system.
* Much better console support (PS4/X1/Switch) which is free (you just have to prove that you have a proper dev account with the console manufacturer), native (no third-party components or engines involved), drop-in (you literally just have to drop in a directory into your project to make it work like any other backend), integrated (creates easy to debug IDE projects for each console plus easy scripts for release-packages), highly-efficient (directly based on the lowest level GPU-APIs on each system) and in the process of being battle-tested (there will be a nice game release based on it this year).
* OpenFL support in http://kodegarden.org so you can show of your creations easily. This is also great for pimping documentation.
* Use Kha's dev tools - cross-platform JavaScript based debugging, runtime code-patching using Krom and whatever else might be cooking...
* Excellent WebGL support, defaults to WebGL 2 and gracefully falls back to WebGL and even to reduced precision shaders on older mobile devices if necessary.
* Reproducible builds if you opt in to use Kha's style of package management (excluding C++ compilation for legal reasons). This is something which keeps putting people off from using Kha but it is super valuable for professional projects. Also, it's optional.
* This whole thing supports more cooperation in the Haxe community. Actually, I think that's the big one.

### Cons:
* Kha's free console support might negatively impact current non-free efforts to get OpenFL and/or Flixel games running on consoles.
* I totally plan to subvert all OpenFL developers into using Kha's own APIs.
* This won't be able to use Kha's &lt;canvas&gt; fallback as it will basically be a rewrite of OpenFL's OpenGL code to instead use Kha's G4 API. The reasonable thing to do will be to fall back to OpenFL's own non-WebGL browser support when WebGL is not available.
* Performance will stay the same for the same reason - this won't change how rendering works in OpenFL. I can sure help with performance later on but that's not part of this pitch.

Choose wisely, I’m anxious to find out whether there’s enough demand for this to justify this large investment.
