---
layout:     post
title:      khamake & koremake
date:       2015-02-20 21:27:00 +0200
author:     Robert Konrad
authorlink: http://robdangero.us
permalink:  khamake-koremake
---
hake and kake have recently been replaced with khamake and koremake. Those are ports of the original tools to [node.js](http://nodejs.org) so you'll need to install that to use them from the command line. You don't need to install node.js when you use Kit because that itself is based on node-webkit (which is now called NW.js) which basically includes node.js. The tools still support all the same options and Kha and Kore include shortcut scripts - a typical call is now `node Kha/make` or `node Kore/make`. The switch to node makes it easier to provide updates of the tools and in the long term will provide a deeper integration with Kit.
