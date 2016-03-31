---
layout:     post
title:      Breaking News 5
date:       2015-04-19 05:23:00 +0200
author:     Robert Konrad
authorlink: http://robdangero.us
permalink:  breaking-news-5
---
The Kha repository has been restructured to minimize download sizes. Where possible submodules have been replaced with binary only repositories - of course all the corresponding source repositories are still easily accessible on Github and updates to the binary repositories will always mention the corresponding revision of the source archives in new commits. Your git client might get confused by this - when in doubt just redownload Kha.
Kit has also been updated and doesn't anymore cache the Kha directory. Now that the Kha repository is sufficiently small the download cache is an unneccessary complication. Also Kit made a switch from node-webkit to Electron and therefore the system specific Kit repositories have been recreated and you might like to redownload those, too:

`git clone --recursive https://github.com/KTXSoftware/Kit-win.git`

`git clone --recursive https://github.com/KTXSoftware/Kit.app.git`

`git clone --recursive https://github.com/KTXSoftware/Kit-linux32.git`

`git clone --recursive https://github.com/KTXSoftware/Kit-linux64.git`

tl;dr: Redownload all the things.
