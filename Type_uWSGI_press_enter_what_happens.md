# Type uWSGI; press enter; what happens?
Speakers Ashesshsh Laroria and Philip James (both from Stripe)

uWSGI: the thing you use in addtion to Flask or Django to deploy a service to the web.

## This talk will answer the following questions (all at the OS level):
1. How uwsgi handles processes?
2. How does uwsgi handle networking?
3. Why should you use it?

## 1. How does uWSGI handles processes?

### Illustrative example: Catserve (Cats as a Service)
Visit the site, get a picture of a cat.  Hit refresh, get a _new_ picture of a _new_ cat!

input:
`> uwsgi --master --http :8000 --module catserve.wsgi`

(and then press enter)

outputs:
`... spawed uWSGI worker 1 (and the only) (pidL 1221, cores:1`

wsgi is a synchronous protocol. I.e., it will lock the python process (1221, above) while the Flask/Django/whatever executes.  This can leads to some very slow page loads, even on processes that aren't themselves slow.

Okay, so: have uwsgi spawn 2 instead of 1 python worker processes.

(Aside/note: are the python workers spawned from uwsgi children of the uwsgi process?)

## 2. How does uWSGI handle networking?

From the same cmd line output mentioned above:

`port bound to http` <--??

Sockets connect to ports to create connections.

Have uwsgi create a socket to connect to port 8000 (since CaaS is running on localhost:8000)

The OS kernel handles sockets and ports.  Need to use `syscall`s to communicate b/w application and OS/kernel layer.

syscalls used:

+ ???? 
+ bind()
+ listen()
+ epoll_wait()
  + processess are ready and waiting 
+ accept()
  + socket accepts a cnxn request 

uWSGI & all forked python procs all have access to the same file descriptors/sockets.  (B/c of permission inheritance)

All python children processes 'compete' to get each request coming into the main uWSGI socket.  Only one wins.  The rest go back to the `listen()` state.

## 3. Why use uWSGI?

1. Graceful code reloading
   + i.e. roll out new app w/o any noticeable downtime from the user side
     + unlike django runserver (or whatever that cmd is)
   + `sighup` <-- syscall that tells OS processes to 'hang up' if not otherwise occupied, or to exit as soon as done w/ whatever's currently occupying them.
2. Tunability
   + Can specify how many worker processes your app needs
3. Security
   + E.g. what if a request has more than one host specified?  uWSGI apparently knows how to handle this securely.
4. Config files
   + Instead of typing everything out on the cmd line every dang time.
5. Features
   + static file serving
   + max requests per worker
   + queuing systems
   + https & http2 support
   + harakiri mode
   + uwsgitop
   + memory-report
   + async (beta) (only python 3.4+)
   + some sort of caching framework

# Audience questions

Q: Why does uwsgi wait for all workers to exit before reloading?

A: Because forking reasons.

Q: Can you tell us more about the uWSGI caching feature?

A: It's recent, and the speakers referred the questioner to 'the documentation', b/c they don't know themselves.

Q: Is there a limit to how many processes can share the input file descriptor (theoretically or practically)?

A: The THUNDERLOCK (another uWSGI) is a feature that forces workers to not _all_ fight to accept the request, but throttles how many compete at the same time.  But there's not hard limit coded into uWSGI.

Q: What happens to log files when the processes exit?

A: They get re-opened when the worker processes restart (on reload)

Q: HTTP2 support: can you just drop that in & have it work, or do you have to restructure your app?

A: Yes and no.  There's a command line flag that lets you use http2 w/ existing code, but b/c http2 re-uses cnxs a lot more, there's also stuff you can/should be doing in your app code to take advantage of it.
