---
layout:     post
title:      New Kit on the Blog
date:       2014-01-14 23:47:00 +0200
author:     Robert Konrad
authorlink: http://robdangero.us
permalink:  new-kit-on-the-blog
---
A first version of Kit, the companion tool for Kha and Kore, is now available at Github. Clone it for your favorite system like so:

`git clone --recursive https://github.com/KTXSoftware/Kit-win.git`

`git clone --recursive https://github.com/KTXSoftware/Kit.app.git`

`git clone --recursive https://github.com/KTXSoftware/Kit-linux.git`

Kit downloads, configures and compiles your projects. When you first start Kit, it displays a little config screen.

![Kit config]({{ site.url }}/assets/images/kit1.png)

Choose a directory for your projects (this is mandatory) and optionally add commands to call MP3 and AAC encoders (we can't just include these for patent reasons). Those lines might for example look like:

`path/to/lame -S -h {in} {out}`

`path/to/faac -o {out} {in}`

You may then click the Projects button in the upper-left corner.

![Kit projects]({{ site.url }}/assets/images/kit2.png)

Kit gets a list of projects from Github. Before you start downloading, please note that Kit handles git submodules (which we use extensively) in a special way: When Kit first encounters a submodule, it clones it directly in your projects directory and then clones it from there to the actual submodule directory in the currently downloaded project. This way Kha itself and all of its supporting libraries will only be downloaded once. Kit also always checks out the latest revisions of all submodules and does not detach your heads - that's usually great when you're actively working on a project, but it's not so great for older projects - for this case use your regular git tools.
When a Kha project is downloaded, things get easy.

![Kit assets]({{ site.url }}/assets/images/kit3.png)

You can add assets and rooms to configure your project.kha and you can create your application for different target systems which will call hake with the proper parameters.
Just as Kha and Kore itself, Kit will be updated regularly - keep your repositories up to date. The Kit you are seeing now is a reimplementation of a former Java tool using node-webkit and as you might now have guessed, we plan to integrate [HIDE](https://github.com/misterpah/hide).
