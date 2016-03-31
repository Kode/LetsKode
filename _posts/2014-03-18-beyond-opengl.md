---
layout:     post
title:      Beyond OpenGL
date:       2014-03-18 17:23:00 +0200
author:     Robert Konrad
authorlink: http://robdangero.us
permalink:  beyond-opengl
---
Today OpenGL is ubiqitous. It's the primary graphics API of OSX, Linux, Android and iOS. It's supported on Windows if your users have current hardware and drivers. Nonetheless Kha and Kore walk a different path.
OpenGL is a nice enough api, but it has a lot of problems for historical reasons. Function parameters sometimes change their meaning (see glVertexAttribPointer). A lot of internal state has to be handled correctly (see glBind\*). Outdated stuff is still around in some of the many OpenGL flavors (see glVertex).
Simply stated, OpenGL has grown complex. That's hardly a surprise considering that OpenGL is more than 20 years old and never did a clean cut. On the other hand, *Graphics*, the 3D API of Kha and Kore, is designed to be as simple as possible. It is easy to learn, hard to misuse and doesn't carry old baggage around.
It is also this simplicity that makes it easy to retarget the API. Therefore Direct3D support is excellent. Stage3D support is excellent. OpenGL support is excellent. PlayStation Mobile support will shortly be excellent. Being based on Haxe this is especially important for Kha. Wouldn't it be a little sad to use a language like Haxe, that can target so many other languages and then restrict yourself to target only one graphics API?

If you want to stay with OpenGL regardless, at least check out [Regal](https://github.com/p3/regal) to get rid of the differences in different OpenGL versions and [ANGLE](https://code.google.com/p/angleproject/) to get rid of the differences in different GLSL versions and to add Direct3D support, which is still very important if you target a more casual audience. And check out Kore's OpenGL backend - it's a nice OpenGL tutorial in itself. We have no good advice for console support though, that's just tough to do with an api as complex as OpenGL.

Meanwhile [Mantle](http://en.wikipedia.org/wiki/Mantle_(API)) spurred development of 3D APIs. This week’s GDC will see the [debut of DirectX 12](http://schedule.gdconf.com/session-id/828181) as well as a [similarly themed, joint presentation](http://schedule.gdconf.com/session-id/828316) by AMD, nVidia and intel about OpenGL. So all we talked about is soon to be kind of outdated. This is how Kha/Kore will deal with this situation: When the dust settled on the new graphics APIs, a *Graphics4* interface will be added. The current *Graphics* interface will be renamed to *Graphics3*. The current *Painter* interface will be renamed *Graphics1*. *Graphics2* is reserved for an interface that can support pre-shader 3D graphics. There will be a *Graphics3* implementation based on *Graphics4*, the same way Kha now includes a *Painter* implementation based on *Graphics* (the *ShaderPainter*). That way the newest bling-bing will always be available in a clean manner while still providing support for older hardware/software without spreading compatibility code throughout the complete system.
