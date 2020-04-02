Coproducts, sum types
=====================

Let's review Costruction of product, before delving with its dual, by reversing arrows and building the coproduct. It's a common topic in Category Theory: we will see Monads and Comonads, Monoids and Comonoids, Limit and Colimit and so on. So, maybe Initial object should have been called Coterminal Object.

Definition of product: a product between `a` and `b` is an object `c` with 2 morphisms `p` and `q` with `p : c -> a` and `q : c -> b`. There are a lot of objects with morphisms to `a` and `b`, but `c` is "the best one" because if we take any other `c'` which also has projections `p'` and `q'` there is a *unique* mapping `m` which will make the triangle 'c' -> c -> a' commute.

## Coproduct
Now, let's reverse the arrows:

```haskell
a    b
\   /
i\ /j
  c

i : a -> c
j : b -> c
```

`p` and `q` would be called *injections* instead of *projections*.

Let's try to find the "best" Coproduct, by reversing the arrows of the Product example.

```haskell
i' : a -> c'
j' : a -> c'

m : c -> c'

i' = m . i
j' = m . j
```

`c'` is the false coproduct, and `m` is unique.

Note from `p' = p . m` and `i' = m . i` that not only we do reverse the arrows, we also reverse the compositions.

We know that a product is in programming: it's a cartesian product, a pair. What a coproduct is in programming? It's a Sum Type.

The fact that we have the injections `i` and `j` means that we are embedding the set `a` in `c` and the set `b` in `c`. Since this is a universal construction, we want this injection to inject the whole thing. So, `c` is a set that contains both `a` and `b`, with no missing information and no extra information. All other `c'` would miss some information or would have some extra elements. `c` would define the ideal sum of `a` and `b`.

The question is what happens when `a` and `b` overlap, for example if `a = b`. Ideally, we could tag each element (this comes from the left, this from the right). That would be a discriminated union.

```haskell
c = (aLeft | aRight)
```

In this case, `m` would map from `aLeft | aRight` to `a`, and it would be non injective, because 2 different elements (one from the left and one from the right) would be mapped to the same element `a`. The opposite wouldn not be possible: `m` from `a` to a discriminated union would not be possible, because a function cannot map a single item to 2 elements in the domain. The discriminated union is therefore more general than `a`.

## Union Types
In terms of types, this is called Tagged Union, or Discriminated Union Type, Sum type, or Variant.

The union between `Int` and `Boolean` is something that is either an integer or a boolean, not both; in the case of product, the pair is both.l

The simplest case of union type is an enumeration, which can be either this or that (in this case, of the same type).

## In Haskell: Either and Pattern Matching
Let's do this in Haskell

```haskell
data Either a b = Left a | Right b
```

It means: you can construct elements of this type either by calling `Left` providing it with an element of type `a`, or by calling `Right` providing it with an element of type `b`.

So, `Left` and `Right` really correspond to the morhpisms `i`, and `j`: one injects `a`, the other one injects `b`. In a pair I had 2 descructors (projections), `fst` and `snd`. Here we have 2 costructors (injection).


How can we extract an element from a Sum type? If we have an element `x :: Either Int Bool`, we cannot just ask *give me an Integer*, because maybe it's not an integer, and it's a boolean. So, in order to deconstruct an object like this we have to take into account both possibilities, with Pattern Matching

There are 2 ways. One is to define a function twice:

```haskell
f Left a = ...
f Right b = ...
```

and the other one is to use Pattern Matching:

```haskell
f e = case e of
    Left a  -> ...
    Right b -> ...

```

With Product Types and Sum Types we have the foundation of a type system. Product Types are the most visible ones in programming languages. Almost every programming language has Product Types, called with different names, like pairs, or classes with fields.

In Haskell a pair can be redefined and given a different name:

```haskell
data Point = P Float Float
```

It is a pair, just like `(Float, Float)`, but has a different name and is actually a different type. We can also give names to the single arguments, with Record Syntax:

```haskell
data Point P = P { x::Float y::Float }
```

It's still a Product. These are differences in the syntax, very useful in programming, but they correspond to the same mathematical concept.
