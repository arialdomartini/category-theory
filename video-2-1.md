Functions, epimorphisms
=======================

## Operational and Denotational Semantics
Operational Semantics: a category of formal programming language semantics in which certain desired properties of a program (such as: correctness, safety and security) are verified by costructing proofs from logical statements about its execution rather than by attaching mathematical meanings to its tems.

Denotational Semantics (or Mathematical Semantics): is an approach of formalizing the meaning of programming languages by constructing mathematical objects (called "denotations") that describe the meaning of experssions. Denotational Semantics is concerned with finding mathematical objects that represent what programs do. An important tenet of Denotational Semantics is that semantics should be compositional: that is, the denotation of a program phrase should be built out of the denotations of its subphrases.

With Operational Semantics we describe how things execute, we define operations of the language, that is how an expression in the language can be transformed in a simpler one.

With Denotational Semantics we map the language in some other area, and we build a mathematical model, we study how language constructs correspond to some mathematical thing. For example, types correspond to sets, and functions to functions between sets.


## Pure, Total and Partial Functions
Mathematical functions are defined for all the domain, not just for some arguments. In programming, we are used to partially defined functions that for some arguments may explode, throwing an exception.

A Total Function is a function defined for all of its arguments. In maths, Total Function is a synonym for Function.

A Partial Function from `X` to `Y` is a function from `f: X' => Y` for some subset `X'` of `X`. It generalizes the concept of a function not forcing to map all the elements of `X`. If `X' = X`, the function is called Total.

### Pure function
A function is pure if it can be memoised, and it can be turned into a lookup table.
