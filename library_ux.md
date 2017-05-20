# Library UX: Using abstraction towards friendlier APIs
Speaker: Mali Akmanalp

Slides available here: bit.ly/abstraction-talk, @makmanalp

## User eXperience
+ "How this makes me feel"
+ Usability

"For Humans", and humans have _feelings_

Good UX:
+ reduces mistakes ("make the wrong impossible")
      + Lots of input params = bad
      + naming inconsistencies (NOUN_VERB and nounVerb in same package methods)
+ minimizes distractions
+ makes complex tasks routine
+ drives adoption

## Abstraction
So: how do we make better UX?
As programmers, we're PRIMARILY in the business of abstractions.

Abstraction is about hiding details in a _controlled_ way.

Hiding details:
+ reduces mistakes
+ makes complex tasks routine
  + as opposed 'butterfly-based disk IO'
+ provides a stable interface

Good abstraction is aligned with good UX!

## Abstraction in python
+ Functions
+ Classes
  + example w/ SQLAlchemy
  + classes make state explicit and organized
  + ... and group state and behavior together

Pitfalls to abstractions:
+ Leaky abstractions
  + fails to conceal all of the details lying 'under the hood'
+ Under-abstraction
  + guts, state, and control-flow everywhere
+ Over-abstraction
  + coupling: to change 1 thing, you have to change all the things
  + cohesion: a thing that tries to do too much at the same time

## Deciding on the level of abstraction
How many layers of it should you have, and what should they each be responsible for?

Tips:
+ Write the press release first.
  + Most generic
  + This guides your abstraction decisions.
+ Write 'imaginary code' second
  + Slightly more concrete, but still generic
+ Then, rewrite usage w/ existing libraries?
+ What does this abstraction cost me? (e.g. coupling, cost of un-doing that abstraction, how likely is this code to change)
+ How does this abstraction benefit the user?
+ DRY: Don't Repeat Yourself, _but also_ Don't Refactor Yet

### Incremental architecture
Good structure comes from domain knowledge... which is a problem b/c you have the least domain knowledge at the outset of a project.  So: BUILD LESS STRUCTURE UP FRONT.

## Tricks of the trade
+ Abstraction != building a wall
  + You want to let users pass optional kw/args to the lower levels of abstraction.
+ Expose intermediate abstraction layers to users (not just the outer layer, as is typical) as fully supported APIs in their own right.

## Conclusion
The right level of abstraction is audience-specific.

Theory: "for humans" adds an abstraction layer we didn't realize was missing before

Abstraction is not a goal; it's a tool.




