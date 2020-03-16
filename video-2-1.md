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

In the language of Category, there is no reference to the elements of the sets: isomorphisms here is expressed only in terms of composition and identity, nothing else.

Isomorphisms are useful when we have 2 sets and for some intent they can be considered identical, because they are isomorphic, there is an isomorphisms that acts like an identification of between these two sets.

For finite sets, an isomorphism is just a mapping between elements. For infinite sets, this is also possible. For example, it's possible to define an isomorphisms between the set of natural numbers and the sets of even numbers:

```haskel
y  =  2x
```
The function is invertible when the domain is the set of even numbers.


There are 2 resons for a function not to be an isomorphism:

* at least two elements of the domain are mapped to the same element of the codomain, that is the function collapses elements of a set; the set of elements that are mapped to the same element of the codomain is called *fiber*;
* the image is a proper subset of the codomain (so, not all the elements of the codomain are covered, the image does not fill the codomain)

```haskell
there exist 2 elements x1 and x2 such that

f x1 = y
f x2 = y

then f is not an isomorphism
```

As for the second reason,

```haskell
there exist a y1 such that

for each x in X

f x != y1
```


### Fibration as abstraction, Isomorphism as modelling
Fibration is very important, because if corresponds to the process of abstraction: when using a function that takes multiple elements from the domain (a fiber) to one single element of the codomain, I'm using the second set as an abstraction of the fist one, that is I'm removing some detail and just keeping some more abstract information, I'm throwing away some information, since by definition I cannot invert the function and know from which element I'm coming from: I'm left on the only information I care about.

Isomorphism is more the process of modelling: I'm modelling a set to another set, which for some intent can be considerd equal; I'm recognizing the pattern that define the fist set inside the second set.


## Injective, Surjective

### Injective function
If a function does not collapse elements it's called injective, it's an injection.

```haskell
for each x1 != x2

then

f x1 != f x2
```

Injective function lead to no abstraction

### Surjective
If the function covers the whole codomain.

*sur* comes from "on", "onto".

### Bijective, isomorphism

If a function is both injective and surjective, it is invertible and it's bijective.

## Category
We defined all above in terms of elements. Let's try to define the same concepts in terms of composition and identity.

| Set Theory | Category Theory |
|:----------------|:------------------------|
| Injective     | Monomorphism  |
| Surjective   | Epimorphism       |


### Epimorphism

In Set Theory, surjective functions. `f` is an Epimorphism if for any object `C` and any pair of `g1` and `g2` follows that:

```haskell
f :: A -> B
g1 :: B -> C
g1 :: B -> C

g1 . f = g2 . f => g1 = g2
```

This is because `g1` and `g2` must be defined for all elements of `B`. If they are obliged to be equal, it means they cannot be any element outside `B` which `f` does not map.

In other words, taking 3 sets `A`, `B` and `C`, if `f :: A -> B` is not surjective, there is a terra incognita in `B` which is not covered by `f`. Having `g :: B -> C`, `g` itself would cover all its domain.<br/>
But, the composition `g . f` would not probe that terra incognita. So, if the equivalence

```haskell
g1 . f = g2 . f => g1 = g2
```

this must mean that neither `g1` nor `g2` probed any elements in this terra incognita, that is, the terra incognita was empty. So, `f` is surjective. In terms of Category, `f` was an epimorphism.

If `f` is not surjective, `g1 . f` can be equal to `g2 .f` even if `g1` and `g2` are different, because their difference would not impact the composition, since it would probe elements which are not elements of `f`'s images.

Note that in

```haskell
g1 . f = g2 . f => g1 = g2
```

it's like I can cancel (simplify) `f` from both the terms, on the right.

Note that for discussing the property without looking inside the Set, we considered the whole universe, and the relation of `f` with all the other morphisms.

### Monomorphism
In Set Theory, injective functions. `f` is a Monomorphism if:

'''haskell
f :: B -> C
g1 :: A -> B
g2 :: A -> B

f . g1 = f .g2 => g1 = g2
'''

If `g1` must be equal to `g2`, it cannot happen that `g1` took to some `b1` and `g2` to `b2` which `f` then maps to the same value `c`.


