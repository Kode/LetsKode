---
layout:     post
title:      WWX News Part 1 - Export to Unity
date:       2015-06-04 18:43:00 +0200
author:     Robert Konrad
authorlink: http://robdangero.us
permalink:  wwx-news-part-1-export-to-unity
---
I did a little talk at [WWX 2015](http://wwx.silexlabs.org/2015/) which showed a bunch of new stuff. That talk will be on YouTube later this month, but meanwhile I'll try to detail all the new features right here in a series of blog posts.

Weird things first, Kha now has a Unity backend. Just call khamake ala `node Kha/make unity` and it will create a proper Unity project. Inside Unity click Kha/Initialize when the project is loaded and you're ready to go. The Unity backend is already almost fully featured, including support for 3D graphics, cross-compiled shaders,...
To make it clear: This creates completely regular Unity projects, there is no special plugin or anything like that. Which means Kha projects can be exported to all targets supported by Unity. Which means **Kha** has full support for **game consoles** right **now**.
