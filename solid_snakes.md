# Solid Snakes: or, how to take 5 weeks of vacation
Speaker: FILL THIS IN LATER

(came into this one 5 minutes late, but)

1. Data normalization at edges
   + pass stuff in as either class objects or dictionaries
   + if you know all the keys in the dictionary, IT SHOULD BE A CLASS

2. Expect failure.  How to plan to operate gracefully with failure?
   + SILENT FAILURES ARE BAD.  You need to have monitoring.
   + Two main types of failures:
     + Local (raises exceptions.  Nice!)
     + Remote (timeouts)
       + Circuit breaker pattern:
       	 + A local proxy b/w your local system and the remote
	   + closed --> open cnxn on failure, with periodic 'tests' to see if the remote is back up yet

3. Redundancy
   Have 2 of everything, unless it's an important system.  Then, have 3.

   E.g. all hitting same DNS provider, or putting all your data in the same availability zone/server farm/etc.

   BACKUPS!  You also MUST test your backups.

4. Docs
   Write down how you do stuff, so other people can do it, too.
   Also: emergency runbooks/checklists are things you should have.


5. Deal with it (when all else fails)
   + Don't make it any worse (cascading failures)
     + e.g. retries-- use exponential backoffs **with jitter** (don't DDOS the endpoint)
          + combinatorial request explosion, which is a real threat w/ microservices systems w/ many layers of dependencies

6. Don't swallow errors

+ Nothing should ever let errors pass silently.

+ A good pattern, if you have app-specific exceptions:
 (roughly, I didn't quite get it all)

```
try:
 foo...
except Exception as e:
  raise AppException() from e 

```

+ Don't try too hard to muddle on in the face of failure.  `sys.exit(1)` is a fine response to a failure.
+ fail fast & loudly.

8. Recovery: make it fast
MTTR: Mean time to recovery

Keep grubby human hands completely OFF of service restorations.


## In summary:
1. Build fault-tolerant systems
2. Turn off your phone.

