---
layout:     post
title:      Kha on haxelib
date:       2015-07-11 03:17:00 +0200
author:     Robert Konrad
authorlink: http://robdangero.us
permalink:  kha-on-haxelib
---
Today saw the first proper haxelib release of Kha. There were some test releases before that didn't work for all targets but that should now all be fixed (if not, please don't just run away - file a bug report).

Kha on haxelib is considerably faster/easier to get started with than the git version. The download is smaller and a Kha directory per project is not necessary. However when starting a real project, using Kha's classic git submodule workflow is highly recommended to properly track dependencies.

Basic usage of the haxelib and git versions is exactly the same with one minor difference: Kha's build tool khamake is normally called ala `node Kha/make html5`. When using haxelib you'll have to instead use `haxelib run kha html5`.

Kha will from now on be updated monthly on haxelib - plus critical patches where necessary. It is versioned accordingly after a year.month.patch scheme. The current version is 15.7.1.
The releases will be accompanied by blog posts detailing everything interesting that happened since the previous version.

To get started, please have a look at the [documentation](https://github.com/KTXSoftware/Kha/wiki), which is recently growing nicely.
To keep up to date on what is planned and what is currently being worked on keep an eye on [Kha's Waffle.io board](https://waffle.io/KTXSoftware/Kha).

Known issues:

* Kha on haxelib is considerably slower than Kha on git for all C++ targets. This is due to some updates to the Haxe compiler and will accordingly be resolved with the next Haxe release.
* Android support is a little broken right now. It is currently being fixed and updated for Gradle/Android Studio.
* VR and multiplayer support is not yet in a usable state.
