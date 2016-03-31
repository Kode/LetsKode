---
layout:     post
title:      WWX News Part 2 - Networking
date:       2015-06-05 15:49:00 +0200
author:     Robert Konrad
authorlink: http://robdangero.us
permalink:  wwx-news-part-2-networking
---
Writing networked multiplayer games is a tough task, even when using some of the bigger game engines (for example Unity really doesn't provide much support for that at all unless you buy some additional third-party plugin). To make a game session robust in the face of potentially unreliable connections and even cheating the complete game should be able to run on a separate server which has final say about the game state. To avoid a game feeling sluggish because of a potentially large distance aka signal travel time to the server the complete game should be able to run on the client to enable proper client side prediction of the game state. So, let's just implement the game twice? Probably not a good idea and therefore Kha can now automatically export a client and a server version of a game after a little bit of necessary metadata has been added.

In detail the process looks like this:
Every synchronized object has to implement kha.networking.Entity and mark synchronized fields as @replicated ala:

	class Block implements kha.networking.Entity {
		@replicated
		public var x: Float = 0;
		@replicated
		public var y: Float = 0;
		private var w: Float = 100;
		private var h: Float = 100;
	}

Every object that receives input data from the player has to implement kha.networking.Controller and mark the functions that receive the input data as @input ala:

	class Keyboard implements kha.networking.Controller {
		@input
		public function sendDownEvent(key: Key, char: String): Void {
            // in here you can use session.me.id to
            // figure out who sent the input event
		}
	}

Of course you don't even have to worry about that when you just use the classes in kha.input directly.
And when all that is done, create a session object and add your entities and controllers ala:

    function startGame(): Void {
		session = new Session(numberOfPlayers);
		session.waitForStart(startSession);
	}

	function startSession(): Void {
	    var block = new Block();
    	session.addEntity(block);
        session.addController(Keyboard.get());
    }

Apart from those few details a networked multiplayer game is implemented just like a local multiplayer game. Kha takes care of the rest. That said, the implementation is still in a very early state and currently only supports the html5 target. Concrete examples will be provided soon, when the implementation stabilizes. Meanwhile feel free to have a closer look at the implementation. Kha has a new Node.js backend and accordingly calling `node Kha/make node` will build the headless server version of a Kha project. The Scheduler has been modified and can now rewind time to reapply received game states or input events to the past. The networking.Entity and networking.Controller classes trigger macros, which pack, send and receive the necessary data in compact byte streams. Macros are the secret sauce of Kha's multiplayer support, providing an api as simple as shown here wouldn't be possible without them.
