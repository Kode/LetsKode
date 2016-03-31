---
layout:     post
title:      Breaking News 4
date:       2014-04-19 16:34:00 +0200
author:     Robert Konrad
authorlink: http://robdangero.us
permalink:  breaking-news-4
---
The startup code for Kha applications changed slightly to make the execution order of the constructor calls clear. The latest Haxe update made that necessary.

The original code, typically in Main.hx, looked like this:

`new Starter().start(new GameName());`

please change that to

`var starter = new Starter();
starter.start(new GameName());`
