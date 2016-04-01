---
layout:     post
title:      WWX News Part 3 - The Slides
date:       2015-06-06 19:41:00 +0200
author:     Robert Konrad
authorlink: http://robdangero.us
permalink:  wwx-news-part-3-the-slides
---
These are the slides from the Kha presentation at WWX2015. The comments are new but mostly similar to the talk (the actual talk will be on YouTube later this month).

![slide1](http://robdangero.us/wwx2015/slide1.png)
It doesn't need any subtitles because it's Kha.

![slide2](http://robdangero.us/wwx2015/slide2.png)

![slide3](http://robdangero.us/wwx2015/slide3.png)

![slide4](http://robdangero.us/wwx2015/slide4.png)
The least popular...

![slide5](http://robdangero.us/wwx2015/slide5.png)
but clearly the coolest of all the Haxe game frameworks.

![slide6](http://robdangero.us/wwx2015/slide6.png)
Hi, I'm Rob, mind buying our games?
Leona: http://store.steampowered.com/app/305880
Redux: http://store.steampowered.com/app/336930
Haunted: http://store.steampowered.com/app/43190
So, I'm a C++ kinda guy and therefore...

![slide7](http://robdangero.us/wwx2015/slide7.png)
Kha is not like Flash. Consequently...

![slide8](http://robdangero.us/wwx2015/slide8.png)
Kha is also not like OpenFL.

![slide9](http://robdangero.us/wwx2015/slide9.png)
It's a low level portability layer, somewhat like Lime or snow.

![slide10](http://robdangero.us/wwx2015/slide10.png)
Kha has two ancestors, first one is Kt, a fancy and portable C++ game engine.

![slide11](http://robdangero.us/wwx2015/slide11.png)
Speaking of C++, it is pretty portable by itself, when you do it right and avoid using unportable utility libraries which try to hide how stuff works.

![slide12](http://robdangero.us/wwx2015/slide12.png)
Kha's second ancestor is Kje, a tiny 2D Java game engine, build for educational purposes.

![slide13](http://robdangero.us/wwx2015/slide13.png)
This was also designed in a portable way...

![slide14](http://robdangero.us/wwx2015/slide14.png)
and worked in the JVM, on Android and in the browser using Google Web Toolkit.

![slide15](http://robdangero.us/wwx2015/slide15.png)
GWT though wasn't that great.

![slide16](http://robdangero.us/wwx2015/slide16.png)
So I was on the lookout for an alternative and did some experiments.

![slide17](http://robdangero.us/wwx2015/slide17.png)
Porting it to Haxe took a day, worked much better for HTML5 and allowed me to merge in parts of Kt to add native backends. Thus Kha was born.

![slide18](http://robdangero.us/wwx2015/slide18.png)
And look where that ended up. It's now the most portable thingamagic in the world. All higher level game engine stuff was moved out though (more about that later).

![slide19](http://robdangero.us/wwx2015/slide19.png)
Kha tries to get four big topics just right, let's have a closer look at each.

![slide20](http://robdangero.us/wwx2015/slide20.png)

![slide21](http://robdangero.us/wwx2015/slide21.png)
Haxe makes cpu-code more portable than anything else.

![slide22](http://robdangero.us/wwx2015/slide22.png)
krafix makes gpu-code more portable than anything else. krafix is a GLSL cross-compiler.

![slide23](http://robdangero.us/wwx2015/slide23.png)
krafix is the successor to Kha's previous shader cross-compiler kfx. It is based on SPIR-V and the GLSL referene compiler.

![slide24](http://robdangero.us/wwx2015/slide24.png)
SPIR-V is Khronos' new shader bytecode that was recently announced together with Vulkan (aka GLnext). krafix cross-compilation capabilities are only loosely coupled to the GLSL reference compiler because they work solely on SPIR-V - therefore easy to support more than just GLSL in the future.

![slide25](http://robdangero.us/wwx2015/slide25.png)
It's a very new thing with some problems remaining. But it's progressing fast and already implementing up to date features that kfx/angle couldn't provide. Tesselation shader support is almost done, first compute shaders are also working.

![slide26](http://robdangero.us/wwx2015/slide26.png)
Compute shaders by the way make it possible to program GPUs in more general ways easier and also provide more synchronization options to make things faster compared to previous shader types.

![slide27](http://robdangero.us/wwx2015/slide27.png)
But almost every system has its own ideas about what a computer shader should look like. Kha is about to solve that problem...

![slide28](http://robdangero.us/wwx2015/slide28.png)
Meanwhile Unity is...really, I don't know what they're doing. Unreal does pretty well though, only missing support for OpenCL.

![slide29](http://robdangero.us/wwx2015/slide29.png)
GLSL in Kha is a slightly modified version of GLSL to make it more portable. Here are two examples (which currently are all the differences, but there might be more in the future).

![slide30](http://robdangero.us/wwx2015/slide30.png)
Hardware accelerated video decoding on most systems doesn't really concern GLSL, because it just returns a pixel buffer that can be copied to a texture.

![slide31](http://robdangero.us/wwx2015/slide31.png)
But on Android hardware video decode writes to a GL_OES_EGL_image thingy. Using that looks somewhat silly in GLSL.

![slide32](http://robdangero.us/wwx2015/slide32.png)
So a GLSL video shader for all systems looks like this. Not pretty.

![slide33](http://robdangero.us/wwx2015/slide33.png)
In Kha accessing a video-texture looks like this.

![slide34](http://robdangero.us/wwx2015/slide34.png)
Tesselation control shaders in GLSL contain the code to define per-patch data and per-vertex data inside one function. Usually per-patch calculations are therefore inside one big if block.

![slide35](http://robdangero.us/wwx2015/slide35.png)
D3D11 instead uses two functions and so does Kha because that can easily be mapped to D3D11 and GLSL.

![slide36](http://robdangero.us/wwx2015/slide36.png)
hxsl, the Haxe Shading Language by Nicolas Cannasse which allows you to write shaders in Haxe syntax directly inside your regular Haxe code, is also supported (but doesn't yet support all of hxsl's features).

![slide37](http://robdangero.us/wwx2015/slide37.png)
Now let's look at the apis and their implementations. Lime and snow implement each api twice, once for SDL/OpenAL and once for HTML5. And graphics - they don't really do graphics, they just forward OpenGL.

![slide38](http://robdangero.us/wwx2015/slide38.png)
Kha on the other hand implements everything for every target. And it has its own graphics api.

![slide39](http://robdangero.us/wwx2015/slide39.png)
For native targets Kha forwards calls to a C++ library that looks and works very similar to Kha and can also work on its own. It's called Kore.

![slide40](http://robdangero.us/wwx2015/slide40.png)
The complete structure looks something like this.

![slide41](http://robdangero.us/wwx2015/slide41.png)
Now, more api details. Kha does in fact have more than one graphics api. I call it a generational api design, there is a seperate api optimized for different hardware/software generations. Currently it's up to Graphics4 with Graphics5 in the pipeline (Metal is already running as a G4 backend right now though and D3D12 is already half-done, too).

![slide42](http://robdangero.us/wwx2015/slide42.png)
Additionaly there are generic implementations of lower level apis targeting the higher levels. So for every of Kha's target the backend implements just the highest possible api and the generic implementations then make the lower level apis available, too. G2on4 might be especially interesting as it provides a high-performance 2D implementation for current graphics hardware. Also G2on4 provides additional api calls, making it possible to use custom shaders in a 2D scene.

![slide43](http://robdangero.us/wwx2015/slide43.png)
So, G2 looks like this.

![slide44](http://robdangero.us/wwx2015/slide44.png)

![slide45](http://robdangero.us/wwx2015/slide45.png)
And G4 looks like this.

![slide46](http://robdangero.us/wwx2015/slide46.png)
The g object seen in the samples can be obtained from the Framebuffer object...

![slide47](http://robdangero.us/wwx2015/slide47.png)
or from an image. So rendering to a texture and then using that is really easy.

![slide48](http://robdangero.us/wwx2015/slide48.png)
Audio is now also a generational api.

![slide49](http://robdangero.us/wwx2015/slide49.png)
Audio1 looks like this.

![slide50](http://robdangero.us/wwx2015/slide50.png)
And Audio2 looks like this. Using Audio2 you can basically do anything you want.

![slide51](http://robdangero.us/wwx2015/slide51.png)
Audio1on2 is a generic software audio mixer and includes ogg playback support (therefore Kha can support ogg playback in for example Safari).

![slide52](http://robdangero.us/wwx2015/slide52.png)
Input...

![slide53](http://robdangero.us/wwx2015/slide53.png)
just callbacks.

![slide54](http://robdangero.us/wwx2015/slide54.png)
The Scheduler is a global object that handles all timing. Callbacks can be scheduled to be executed at a specific game time or per frame.

![slide55](http://robdangero.us/wwx2015/slide55.png)
Assets are handled using a per project config file called project.kha.

![slide56](http://robdangero.us/wwx2015/slide56.png)
Here is an [actual example](https://github.com/KTXSoftware/Ploing/blob/master/project.kha).

![slide57](http://robdangero.us/wwx2015/slide57.png)
In the actual game assets can optionally be loaded in packages called rooms as defined in project.kha.

![slide58](http://robdangero.us/wwx2015/slide58.png)
khamake is Kha's build tool which reads in project.kha and optimizes/compresses all assets for the chosen target platform. It also compiles all Haxe and GLSL code and creates hxproj and hxml files.

![slide59](http://robdangero.us/wwx2015/slide59.png)
koremake is the accompanying build tool for Kore. It's a generic C++ build system but doesn't directly build the project but instead outputs IDE projects. That's one more step to compile the project, but so much more possibilities - debuggers, profilers,...

![slide60](http://robdangero.us/wwx2015/slide60.png)
So how portable is it really, compared to other portable stuff? SDL disqualifies because it doesn't handle graphics.

![slide61](http://robdangero.us/wwx2015/slide61.png)
Monkey is nice but not really up to date when it comes to graphics.

![slide62](http://robdangero.us/wwx2015/slide62.png)
And those things? I really have no idea.

![slide63](http://robdangero.us/wwx2015/slide63.png)

![slide64](http://robdangero.us/wwx2015/slide64.png)
The HTML5 target is really really good. Full G4 support, well performing fallback to canvas,...
Also there is a second HTML5 target. The HTML5-Worker target runs the complete project inside a worker thread and outputs rendering commands to the main thread. Great for avoiding timeouts in long calculations. Also great for embedding Kha inside for example a web-based game editor.

![slide65](http://robdangero.us/wwx2015/slide65.png)
The Kore backend is very straight forwared - g4 and a2 on all native targets.

![slide66](http://robdangero.us/wwx2015/slide66.png)
Some native targets actually support multiple graphics backends. Windows supports three (and soon four). Also, full Win10 support and no d3dx libs needed at runtime (so no directx installation for your clients).

![slide67](http://robdangero.us/wwx2015/slide67.png)
iOS target supports OpenGL and Metal. Also pvrtc texture compression (just add compressed: true to an image in project.kha).

![slide68](http://robdangero.us/wwx2015/slide68.png)
There are actually two Android targets, allthough the Java target is currently not up to date. Support for all the different kinds of compressed textures on Android currently in progress.

![slide69](http://robdangero.us/wwx2015/slide69.png)
On the other end of the spectrum are things like the Java backend. This only supports g2 and a1, but works solely on standard Java apis and can therefore be embedded in Java applications without hassles.

![slide70](http://robdangero.us/wwx2015/slide70.png)
Old backends for Xbox 360 and PlayStation 3 do exist, but currently no devkits at hand. If interested to use that and get it up to date, please get in touch.

![slide71](http://robdangero.us/wwx2015/slide71.png)

![slide72](http://robdangero.us/wwx2015/slide72.png)
Kha is efficient because it doesn't do much. All apis are designed to map to the underlying hardware/software as directly as possible

![slide73](http://robdangero.us/wwx2015/slide73.png)
Also khamake handling assets automatically can help a lot with loading times and memory usage.

![slide74](http://robdangero.us/wwx2015/slide74.png)
Plus because khamake/koremake create IDE projects you have all native tools at your disposal to inspect performance further.

![slide75](http://robdangero.us/wwx2015/slide75.png)
Have [some bunnies](http://robdangero.us/bunnies/)
Sources at https://github.com/KTXSoftware/BunnyMark
Please note the simplified implementation compared to the original version: https://github.com/KTXSoftware/BunnyMark/blob/master/Sources/TileTest.hx
It's just calling drawImage for every bunny. Kha can make that fast automatically in most situations.

![slide76](http://robdangero.us/wwx2015/slide76.png)
Performance is robust but it gets really fast when you optimize for your usecase. G2onG4 makes that easy for 2D - take it and change it. Rotating bunnies can be made much faster by calculating the rotations inside the vertex shader for example (but it's not a good optimization for all situations, for that reason it's not in Kha's G2onG4).

![slide77](http://robdangero.us/wwx2015/slide77.png)

![slide78](http://robdangero.us/wwx2015/slide78.png)
Kha projects are usually handled using git submodules so that every dependency is properly versioned. Even the Haxe compiler itself is just a submodule.

![slide79](http://robdangero.us/wwx2015/slide79.png)

![slide80](http://robdangero.us/wwx2015/slide80.png)
C++ compilers and stuff - just too big and often proprietary.

![slide81](http://robdangero.us/wwx2015/slide81.png)

![slide82](http://robdangero.us/wwx2015/slide82.png)
Introspection, all the way down, always working.

![slide83](http://robdangero.us/wwx2015/slide83.png)
Other code can't just be pasted in, because Kha doesn't clone anybody's apis. So you have to understand what you are doing. But Kha makes that easy, because the apis represent the underlying concepts very clearly.

![slide84](http://robdangero.us/wwx2015/slide84.png)
:)

![slide85](http://robdangero.us/wwx2015/slide85.png)
:(

![slide86](http://robdangero.us/wwx2015/slide86.png)
Now some examples of stuff that runs on top of Kha. ZBlend is a 3D game engine by Lubos Lenco. It includes the bullet physics engine and it integrates with Blender. Even game logic can be defined directly in Blender. http://zblend.org

![slide87](http://robdangero.us/wwx2015/slide87.png)
KhaPunkt is a 2D game engine - a port of HaxePunk, done by Sidar Talei. Has some nice additions compared to the regular HaxePunk. https://bitbucket.org/stalei/khapunk

![slide88](http://robdangero.us/wwx2015/slide88.png)
Those exist on GitHub. Please don't use them. Work in progress.

![slide89](http://robdangero.us/wwx2015/slide89.png)
But this one you can use. It was formerly included in Kha, but I took it out, because I think everybody should choose for themselves which engine to use on top of Kha - if any.

![slide90](http://robdangero.us/wwx2015/slide90.png)
All the links are at http://tech.ktxsoftware.com - also join our IRC channel (and I'm also usually on #haxe at freenode).

![slide91](http://robdangero.us/wwx2015/slide91.png)
And now for the WWX surprise features: Virtual Reality support by Florian Mehm.

![slide92](http://robdangero.us/wwx2015/slide92.png)
Supports basically all devices that are currently available.

![slide93](http://robdangero.us/wwx2015/slide93.png)

![slide94](http://robdangero.us/wwx2015/slide94.png)

![slide95](http://robdangero.us/wwx2015/slide95.png)

![slide96](http://robdangero.us/wwx2015/slide96.png)

![slide97](http://robdangero.us/wwx2015/slide97.png)
Watch the [SteamQuest trailer](https://www.youtube.com/watch?v=JCicZeHO5ew).

![slide98](http://robdangero.us/wwx2015/slide98.png)

![slide99](http://robdangero.us/wwx2015/slide99.png)

![slide100](http://robdangero.us/wwx2015/slide100.png)

The other surprises were [Multiplayer support](http://tech.ktxsoftware.com/wwx-news-part-2-networked-multiplayer) and [Unity export](http://tech.ktxsoftware.com/wwx-news-part-1-export-to-unity) (there were no slides for those to avoid leaks).
