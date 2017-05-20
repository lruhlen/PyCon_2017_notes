# How to make a good Python library API
Speaker: Flavio Juvenal

Not just web apps have APIs.  This talk covers APIs for modules/libraries.

A good API: makes it easier to develop a solution by providing building blocks to be put together by the programmer.

An API is a UI. Think about the humans that will use it.

Requires:
1. Simplicity
2. Flexibility
3. Consistency
4. Safety

This talk covers the first 2

python.apichecklist.com <-- online tool he made. CHECK THIS OUT!

## Simplicity

### Focus on the 90% use cases
Use a 'top-down' design approach

Example:
90% of users call a function/use a class
10% call functions/inherit classes to chage attrs, or call functions intertwined  w/ custom logic/ inherit classes to change methods, fork

The 90% = simplicity
The other 10% = flexibility

#### Start with a README
1. Pitch to your users
   + why this library exists?
   + what problem does this solve, and to what extent?
2. Show users how to use the library
   + sample code for most common use cases
3. Know your users-- ask them!
   + Ask them what they need, and ask them to use your API
   + Measure how the API is being used, to determine what those 90% of users are doing.

#### Progressive disclosure
   + Example: Google.com UI
   + Present the simple, most common use cases first.
   + Provide the more complicated, specialized stuff 'further down'
   + Need to have good default values to make progressive disclosure work well!
     + Require making assumptions

#### Avoid cumbersome imputs (remove clutter)
+ Check if user is instantiating just to call your API
  + If so, change that!
  + Add a method to the API that instantiates that thing 'under the hood' in the library API

#### Use abstractions to simplify
But not too much abstraction, to the point of being cryptic.

Don't focus on 'how'. Focus on 'what' (the task is doing).  'What' >> 'How'

Brevity: Good abstraction reduce clutter & verbosity

Law of leaky abstractions: all abstractions leak.  It's impossible to abstract perfectly. Better to embrace complexity than to create complicated situations.

Example: RPC vs. REST (I didn't entirely follow this)

#### Be Pythonic
Pythonic APIs look like each other.  Users should recognize rather than recall how to do an operation w/ your library API.


## Flexibility
"Make the 10% possible"

### Integration discontinuity
Solutions to problems range from 'simplest possible fix' to 'way overkill'.
If your only option is 'way overkill', you have integration discontinuity.

To solve:
+ increase the granularity of your API.
  + Do this by enforcing seperation of concerns.
+ Have multiple levels of abstractions
  + e.g. have both method and decorator options to call a function
+ Increase opportunities for extensions
+ attribute vs. method smell
  + methods are more flexible than hard-coded attributes (in class definitions)
+ Be pythonic:
  + duck-typing rather than adaptors
  + don't use `type ` or `isinstance` to interact w/ client objects.  Just call 'em.
  + there's a long laundry list of things to do

## In conclusion:

"Make the simple easy, the complex possible, and the wrong impossible."
