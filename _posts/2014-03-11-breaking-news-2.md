---
layout:     post
title:      Breaking News 2
date:       2014-03-11 02:25:00 +0200
author:     Robert Konrad
authorlink: http://robdangero.us
permalink:  breaking-news-2
---
hake generated hxml files now require you to cd into the build directory before calling haxe. This was of course done to make a new feature possible: Flash asset embedding. If you add the parameter embedflashassets to your hake call, the Flash asset Loader will be switched to a different mode and an Assets.hx file will show up in your Sources directory. That Assets class is the reason for the hxml change - for that to work, haxe and FlashDevelop have to search for assets in the same path.
