---
layout:     post
title:      New Graphics
date:       2014-08-21 17:16:00 +0200
author:     Robert Konrad
authorlink: http://robdangero.us
permalink:  new-graphics
---
A new graphics api just landed on Github. Graphics apis are now numbered:

* graphics1 will be a super basic pixel pushing api (not yet implemented)
* graphics2 is a higher level 2D api (based on the previous Painter api)
* graphics3 will be a 3D api for older hardware (not yet implemented)
* graphics4 is a shader based 3D api (based on the previous Sys.graphics api)

The old 2D api is still available in kha.deprecated.Painter to make the transition easier. The [deprecated_painter branch of BlocksFromHeaven](https://github.com/KTXSoftware/BlocksFromHeaven/tree/deprecated_painter) shows how to use it.

Game.render now gets passed a Framebuffer object. You can draw to the framebuffer like this:

`

	override public function render(frame: Framebuffer): Void {
		var g = frame.g2;
		startRender(frame);
    	g.drawImage(image, 0, 0);
		endRender(frame);
	}`

This however will not scale your frame automatically like the Painter interface did.
But the old scaling behaviour can easily be achieved using the new Scaler class:

`
	
    class MyGame extends Game {
		var backbuffer: Image;
    	override public function init(): Void {
    		backbuffer = Image.createRenderTarget(640, 480);
    	}
    
    	override public function render(frame: Framebuffer): Void {
    		var g = backbuffer.g2;
        	g.begin();
			g.drawImage(image, 0, 0);
			g.end();
        
			startRender(frame);
			Scaler.scale(backbuffer, frame, kha.Sys.screenRotation);
			endRender(frame);
		}
	}`

This also demonstrates how easy it is to draw to an image using the new graphics apis.
