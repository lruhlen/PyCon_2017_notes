# Yes, it's time to learn regular expressions
Speaker: Al Sweigart

Slides available at: bit.ly/yesregex

What are regexs useful for?  Text pattern matching.

Compile, search, and group:
```
import re
myreg = re.compile(regex pattern)
foo = my_reg.search('string you are searching through')
print foo.group()
```

### Basics
The `r'...'` makes the following regex text 'raw strings', so you don't have to escape backslashes.

Regexs are complicated, but better than writing a million lines of if/else statements to check for pattern match.

Character classes: digit (or not), word (or not), space (or not)

You can create your own character class by putting characters within square brackets.

If you're searching for any punctuation mark chars, must escape them w/ backslashes in the regex

Curly braces enclosing a number = number of repeats of pattern you're looking for (e.g. 3 consecutive digits --> `\d{3}`). Pattern, then quantity.

`*` = zero or more, `+` = one or more

### Groups
Can group together several pattern match regexs w/in parens, and then specify a quantity after + outside the parens

Helpful websites:

http://pyregex.com, http://regexr.com <-- online regex testing tools


### Alternatives with pipes:
Match 'foo' or 'bar' or 'baz', in any order they appear in the string.  Pipes = `OR`.

## What Regexes Can't/Shouldn't Do
+ Don't parse html with regex
+ Don't parse JSON with regex
+ A regex for strong passwords
  + It ends up being huge
  + Just break it up into multiple regexes
+ Matching nested parentheses
  + Because regexs ain't programming languages

## Audience Questions

Q: Do you have a good usecase for look-aheads

A: Yes! Find-and-replace. Use the pattern you found (earlier in the regex) later in the regex.  Use the `\1`, `\2` to refer to the first, second, etc matches that were found






