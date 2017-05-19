# In-memory event resequencing: Realistic testing for impossible bugs
(Speaker: Glyph)

Because: distributed systems are hard, and they're now ubiquitous.

Signs you're building a distributed system:

+ if `import requests` is in your code

**For example:**

In-game purchases with real money.

Uses threads to speed up payment process.  Easy, right?
But if one thread blocks other stuff: players can steal!

Okay, so: use a state machine to keep track of whether ppl owe money, or are in good standing.
But alas: there's still a race condition that players can exploit for gamebux.

Okay, so: use thread locks!

But: how to test this?

1. Use a fake lock
	+ But: running code logic in sequence is never the same as running in parallel

2. Use end-to-end tests
	+ Good for _discovering_ bugs, but not for _reliably reproducing_ bugs

3. Simulate the passage of time 
	+ Give race conditions a time window to show up.
	+ "verified fake"
	+ `twisted` module 
	+ Lets you manually control the system clock advances.
	+ something about a `SynchronousTestCase` method in `twisted`
	+ "These results are 100% real"
	
(Aside: he's talking about 'concurrency' and 'futures' and 'defereds' and it's going over my head.)

4. Simulate traffic on the network
	+ also using some `twisted` module: `treq.testing`
	+ Simulate web servers and clients, but with enough determinism in the behavior to be useful as a test.
	+ Can unit test server results, regardless of the order in which those events fire/return.
	
(Aside: apparently `await` is something you can use, kind of like `while`.  Not sure if this is `twisted`-specific.)


	
