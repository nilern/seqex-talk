# About Me

* Elaborate on list items
* Wrote a blog on this, now we are here for a different format
* Hard to create grand vision while busy with challenging work
* Haven't actually been programming much for the last month or so
* Anyway you can find my stuff at GitHub

# Regex vs. Seqex

# Regex Operators

* Normal regex and Malli seqex syntaxes
* Elaborate on list items
* Last three can be expressed in terms of the other ones

# Expressivity

# Requirements

* Elaborate on list items

# Staying Regular

* Recursive specs => regex -> EBNF
* So you can express context free languages, not just regular ones
* Here we have an S-expression parser
* Not possible to match nested parens like this with regular expressions
* If you are going to allow any CFG you should actually handle every CFG gracefully
    - Left recursion (stack overflow in Spec)
    - Ambiguous grammars (should probably return all possible parse trees like Instaparse)
* Ambiguous schemas probably not desirable
    - But no good way to disallow them either
    - e.g. LR parsing disallows ambiguity, but also all nondeterminism
        * And the error messages are bad (shift-reduce conflicts)

# Possible Algorithms

* Regular expressions ~ regular grammars ~ FSMs
    - Deterministic
    - Nondeterministic (to generate DFA (Lex) or directly (Seqexp))
* Backtracking parser (overpowered, not as efficient)
* Regex derivatives (to generate DFA (Racket Lex) or directly (Spec))

# Comparing Algorithms

# PikeVM Thread Deduplication Breakdown

# Base Parsers

* Implementing backtracking parsing, parser combinator style
* `validate`, `explain` and `encode`/`decode` are similar
* `unparse` is straightforward, unrelated to all this fancy CS stuff
* Explain code

# Unit & Functor Parsers

* Used to implement some of the other parsers

# Concatenation Parser

* Category theorists: by ading this, parsers form an applicative functor
    - Monad not needed to parse regular or even context free languages

# Alternatives Parser

# Kleene Star Parser

# Repeat Parser

* Similar to Kleene Star parser but need to track the count
* Could concatenate `min` copies of `parser` and `max - min` copies of
  optionalized `parser` instead like in Seqexp
    - But that could get quite big
    - Being able to avoid that is a bonus benefit of switching to this approach

# Derived Parsers

* Like `:repeat`, these can be implemented with existing combinators
    - And unlike `:repeat`, no reason not to

# A Gotcha

# Base CPS Parsers

* No `call-with-current-continuation` in Clojure
* So to get the continuation we need to CPS convert the parsers manually
* Explain code

# CPS Unit & FUnctor Parsers

# CPS Parser for Kleene Star

* And to keep the Kleene star and `:repeat` loops as loops (not using stack space)
  the overall parsing process needs to be trampolined
* And the trampoline also gets access to the continuation inside the loop here
* In case the latter statement fails, the trampoline also exits the loop by
  calling the upper ('fallback') continuation

# CPS Parser for Repeat

# CPS Parser for Alternatives

* Again the trampoline takes care of the 'fallback' path

# CPS Parser for Concatenation

# CPS Driver (Trampoline)

# Memoization

# Performance

* So it is (was) 10 times faster than Spec
* But 20 times slower than the less general `:sequential` schema

# Assessment

* Elaborate on list

