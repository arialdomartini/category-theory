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

## Composability
First we want to decompose the big problems into little blocks, and then recompose stuff from there. In Functional Programming, we eventually come to the bottom, which is composed by pure functions (and types). On top of pure functions we can build more complex stuff, including I/O.


## Morphisms, Relations and Functions
We will look to Total Pure Functions as Morphisms in the Category Set. Category Set contains Sets and Morphisms (Functions) between Sets.

A Function from `S1` to `S2` in mathematics (in Set Theory) is a special kind of relation:

* it's a set of pairs of elements
* the relation does not have to be symmetric

Cartesian Product between `S1` and `S2` is the Set of all the possible ordered pairs of elements from `S1` and `S2`. A Function is a subset of that Cartesian Prodcut which includes all the elements of `S1`.

Note that the pairs are ordered: that is, there is a directionality, which we might represent with arrows between elements of `S1` and elements of `S2`.

It is still OK for multiple elementes in `S1` to be in relation with the same element in `S2`. All the elements of `S1` must be taken into consideration; however, it is not necessarily true that all the elements in `S2` are covered.

`S1` is called Domain, `S2` is the Codomain. The subset in `S2` covered by the function is called Image.

Multiple elements from the Domain can be associated to the same element in the Codomain, but not vice-versa: multiple elements of the Codomain cannot be associated to the same element in the Domain; in other words, each element of the Domain must be associated to a single element of the Codomain.


> Mappings between Sets are called Functions
> Mappings between Categories are called Functors
> Mapping between Functors are called Natural Transformations
> We will see all of this later.


# Injective, Surjective and Bijective functions

```haskell
f: a -> b
g: b -> a

g . f = id

then 

f is invertible
```

or

```haskell
f(g(x)) = x  for each x
```

If

```haskell
g . f = id

then 

f . g= id

because

g . f. = id
g . f . g = id . g
g . f . g = g
g . f . g = g . id
f . g = id
```


## Isomorphisms and invertible functions
A function that is invertible is called *Isomorphism*.

`f` is an isomorphism is there exist a function `g` so that:

```haskell
f :: a -> b
g :: b -> 

f . g = id
g . f = id
```

In the language of Category, there is no reference to the elements of the sets.


