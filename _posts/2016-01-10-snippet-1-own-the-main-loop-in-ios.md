---
layout:     post
title:      Snippet 1 - Own the Main Loop in iOS
date:       2016-01-10 19:04:00 +0200
author:     Robert Konrad
authorlink: http://robdangero.us
permalink:  snippet-1-own-the-main-loop-in-ios
---
When writing graphical applications there are typically two ways to drive the display. Either one can tell some other piece of software to call back when a new image is required

```
requestAnimationFrame(myFancyDrawingFunction);
```

or one takes control of the rendering loop itself.

```
while (true) {
	doSomeStuff();
	
	// Handle os events and the like.
	// If you don't do this regularly,
	// the os will generally assume that
	// your application is not responding.
	systemEvents();

	// Feed some work to your GPU
	myFancyDrawingFunction();
    
	waitForVSync();
}
```

The former method seems to be more common nowadays and is mandatory for JavaScript running in a web browser. C/C++ though is all about control and in that context one typically doesn't want to give up control of the main loop. Kore allows both styles of writing a program and controlling the main loop currently works everywhere but in the JavaScript/Emscripten target. But on some systems it is hard to find documentation on how to achieve this. The primary offender is Apple's iOS.

Today Apple suggests to use the displayLink api to hand over a function pointer for the system to call. In earlier times Apple suggested to use plain system timers - an unreliable method that made it easy to miss a frame. But contrary to all of Apple's suggestions it was always possible to take over the control of the main loop.

The following code expects you to be familiar with the standard procedures to create and run an OpenGL or Metal view in iOS. You can read up on those in Apple's iOS documentation or just create a sample project in XCode.

Your main entry point looks like it always does, for example like this:

```
int main(int argc, char** argv) {
	@autoreleasepool {
		return UIApplicationMain(argc, argv, nil, NSStringFromClass([KoreAppDelegate class]));
	}
}
```

Nothing special so far, but the AppDelegate looks somewhat different as we have to implement the application:didFinishLaunchingWithOptions: method:

```
- (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions {
	// You can create your view right here
	[self performSelectorOnMainThread:@selector(mainLoop) withObject:nil waitUntilDone:NO];
    return YES;
}
```

This will run the mainLoop method on the actual main thread. Consequently you can put the actual main loop inside this particular method:

```
- (void)mainLoop {
	@autoreleasepool {
		while (true) {
			doSomeStuff();
			systemEvents();
			myFancyDrawingFunction();
			waitForVSync();
		}
	}
}
```

You can of course put your loop in a separate plain C function and call that to keep the Objective-C code out of your application code.
Only two things are missing now - we have to implement the systemEvents and waitForVSync functions. They look like this:

```
void waitForVSync() {
	[view end]; // view is your actual UIView that contains your CAEAGLLayer or your CAMetalLayer
}
```

```
void systemEvents() {
	SInt32 result;
	do {
		result = CFRunLoopRunInMode(kCFRunLoopDefaultMode, 0, TRUE);
	}
	while (result == kCFRunLoopRunHandledSource);
	return true;
}
```

It's easy when you know it. This way you stay in control and never miss a frame unless you want to. It all works fine with OpenGL and Metal and doesn't use any non-public apis.
