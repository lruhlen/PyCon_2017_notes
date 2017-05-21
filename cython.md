# Cython as a game changer for efficiency
Speaker: Alex Orlov (of Instagram)

Python is great, but not great with CPU & memory usage.

Profile your code, to see if you even need to work on making your code more efficient.

Then, check the algorithm in your code.

Other ways to speed up your code:
+ microservices
  + but, increases complexity
+ C extensions + python bindings
  + But, you have to use C
+ Change the python runtime (PyPy, Pyston, GrumPy, etc.)
+ Update Python
+ Use Cython!

Cython is:
+ works w/ both python2 and python3
+ compiles C and/or C++
+ mostly looks like Python
+ Can just write python code, then compile it to C using Cython.
+ You can (optionally) add types (to the Python that will be compiled)
  + Can get 200x speedup. (HOLY COW!!!)

## Cython brief dive
### `cdef`
Used to assign type to variables
### function signature
Assign types that functions accept and return
### function declarations
+ `def`
  + standard python function def
+ `cdef`
  + will compile funct ONLY to C (will not be available to call in Python)
+ `cpdef`
  + will generate both native C funct and a python-callable version of the funct

All standard C types are available. Also handles all types of Python collections (set, list, dict, etc).  Also supports low-level C types (c-arrays, pointers, etc)

### Extension types
Looks like Python classes.  Lets you use Cython vars (less memory overhead) in python classes.  They can be inherited, too.

## Gradual optimization:
1. detect critical module
2. compile it
3. add types
4. add additional optimizations (optional)

Instagram results so far:
+ 10-ish modules converted so far
+ 30% CPU improvement
+ and they're not even fully rolling w/ this conversion yet!

Often used to wrap external C libraries, or for data science stuff.  But it's really helpful for regular development, too.



