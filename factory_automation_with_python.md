# Factory automation with Python

Sensing + actuation + brains = automation.

Demonstration of using a library to read barcodes on packages.  Interfaces w/ the barcode reader machine.

The `__enter__` and `__exit__` methods in your class definition.  These somehow provide context management, which is somehow important for this sort of thing.

Caveats:
+ Serial cables only works up to 50ft.
+ Your server doesn't have enough seriel ports

`xmlrpc` <-- xml remote proceedure call.  Runs your python code as a server on the network.  So now, you can serve these USB parser class(es) over the network, and not be limited to 50 ft.

1. Industrial automation exists
2. Python works fine for interfacing with it (pure Python, no C or anything)
3. Python's included "batteries" are uesful here
4. Results are often more elegant & efficient than what the vendors themselves provide.

"API" docs for physical devices are often... basically circuit diagrams.

Programmable logic controller (PLC) <-- these devices basically run factories (?)
  + Usually have a simple OS
  + real-time kernel
  + library of slices for signal types (an 'alphabet')
  + looking for PLC variables that read/write voltages to the network, and are writeable
  + pyads (automation device specification).  Wrapper around vendor supplied C library.
    + also: counsyl-pyads

Here, he uses these tools to turn a little conveyor belt on & off, w/ a rubber duck on it.  The duck bites it, repeatedly.

Next, he does a live demo of a 'sort chewing gum packages by color, and also read their barcodes' using the same little conveyor belt.


Interesting conundrum: factory devices are by definition singletons, and their state(s) aren't mutable.  (Once you start the 'shake' process, it's going to continue that for a minute, no matter what you do.)

The architecture of these systems end up looking identical to microservices.

## Want to get started?
The field is currently wide open.  Get in there!

1. Device drivers: apis for robots
2. File formats & protocols: parsers, converters, viewers
3. Data science and machine learning: vibration monitoring, predictive maintenance, scheduling optimization
4. Security: you'll be buys...

## Packages used
+ pypi: pyserial
+ pypi: microscan
+ pypi: pyads
+ github: chwiede/pyads
+ github: counsyl/counsyl-pyads

+ Barcode reader: Microscan MS3
+ conveyor belt: Dorner 1100 Series
+ PLC: Beckhoff CX 1020