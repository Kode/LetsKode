---
layout:     post
title:      Breaking News 1
date:       2013-12-29 04:55:00 +0200
author:     Robert Konrad
authorlink: http://robdangero.us
permalink:  breaking-news-1
---
Today's changes are purely versioning related. Recently hxcpp (the Haxe C++ support lib) moved to github. It was the last project which Kha depends on, that was still versioned using svn. Our forked repository was of course incompatible, so we created a fresh fork and reapplied our changes. But that makes your clone incompatible, too and you can not just pull the latest changes.
The easiest thing to do, which avoids any submodule hassles, is to rewire your kxcpp repositories (in projectname/Kha/Backends/kxcpp) by fetching and then resetting to a commit in the new master branch like so:

`git fetch
git reset --hard bcfe4d5`

When this is done you can again pull as usual, which will also get you the very latest Haxe version.
