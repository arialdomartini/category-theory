Functors
========

## Motivation
Functors are important to define Natural Transformations, which we will see in the future (9.1).

Mathematically speaking, it's a mapping between 2 categories.

In the previous chapters we referred to patterns, as structures. A pattern can be a catogory in itself. Wiht this in mind, pattern matching is the ability of recognizing a category inside another category. We will come back to this when we will discuss about limits and colimits, when we will see that products and co-products are just examples of limits and co-limits.

When mapping between categories, we will see one category as the model, and we recognize the model inside another category. This is the motivation for functors.
    
## Functors
Let's start from a simple category, in which objects form a set. A mapping between this category and another simple one is just a function, a mapping of sets. All the things we know about functions (being or not being surjective, or injective) just translate to Functors.

Here we are interested in mappings that preserve structures. Functions are really primitive in this sense, because Sets don't have structure, they are just a bunch of elements. But categories have structure. A category embodies structure.

### Preserving structure
A Set can be represented by a category with no morphisms other than identities. It's called Discrete Category. Any category that is no discrete has a structure.

If we want to preserve structure, our mapping must also map arrows.

Let's call the functor `F`. The functor maps objects from left category to right category.

```haskell
a -> F a
b -> F b
```

It also maps the morphism `f : a -> b` to `F f : F a -> F b`. This is what preserves the structure.

The homset `C(a, b)` on the left is mapped to `D(F a, F b)`. Both the homsets are sets. So, a Functor is a function, between objects and between hom-sets.

Structure is connected to composition. Functors should preserve composition. Let's see this. Say we have

```haskell
f :: a -> b
g :: b -> c

g . f :: a -> c
```

Applying the Functor:

```haskell
F f :: F a -> F b
F g :: F b -> F c

F g . F f :: F a -> F c
```

and, importantly, `F (g . f) = F g . F f`. That's what we call preservation of structure. In order to be a Functor, this must be valid.


## Identity
```haskell
ida : a -> a

F ida = idFa : F a -> F a
```

Not every `F` grants this. In order to be a Functor, this must be granted.

So, a functor is a mapping of objects and morphisms that preserves composition and identity.

## Functor properties
Functors needn't be surjective. It's possible that some morphisms on the source category have no correspondent morphism in the target category. They don't neither need to be injective. We can drop some information when we map from a category to another. But they can never destroy or break connections: in topology, we would say that they are a continuous transformation. There is the topic of continuous functors that defines this more precisesly.

### Faithful and Ful Functors
We can define Functors that don't shrink things. A Functor injective on hom-sets is called Faithful.

A Functor that is surjective is called Ful.

Here we talk about hom-sets, not objects! A Faithful Functor can collapse objects.



### Functor from singleton category
If we take a category with only 1 object, what a Functor from it could be? It must map identity.

### Constant Functor
It's a Functor that collapses every objects in single object It's a like a black hole. All the morphisms in the source category are mapped in the identity of a single object in the target category.

## Endofunctors and type constructors
Let's translate all of this in programming.

In programming we deal with a single category, with types and functions. In principle, a Functor can map to the same category: in this case it's called endofunctors.

In Haskell endofunctors are just called Functors.

Objects are types, morhphisms are function.

We have a total mapping of types. The construct to use in Haskell is called Type Constructors, in other languages is called parametrized data type, or template, or generic types. We are talking of the family of types that are parametrized by other types.

This is just one part of a Functor. But we also have to have mapping of morphisms, that is functions.

```haskell
data Maybe a
```

For every type `a` we have to define a type `Maybe a`.

The functor `Maybe` maps `a` into `Maybe a`. This is the mapping of type: `Int -> Maybe Int`.

In Haskell that's defined as:

```haskell
data Maybe a = Nothing | Just a
```

It's a coproduct.

Is this a Functor? Let's see how it acts on hom-sets.

`b -> Maybe b`. If we have `f :: a -> b`, this `f` would be mapped by `F` into a morphism in the target category.

```haskell
F f = fmap f
fmap f :: Maybe a -> Maybe b`.
```

So, `fmap` for `Maybe` is a function that takes `f : a -> b` and produces another function `fmap f :: Maybe a -> Maybe b`. `fmap` is defined differently for every functor. In Haskell all the `fmap` for all the functors have the same name `fmap`: it's a polymorphic function.

Let's try to implement it:

```haskell
fmap :: (a -> b) -> (Maybe a -> Maybe b)
```

`fmap` takes `f`, and produces a function that goes from `Maybe a` to `Maybe b`. Let's give it a `Maybe a`. `Maybe a` can be either `Nothing` or `Just a`. So, we have to take the 2 cases into consideration. Let's start with `Nothing`:

```haskell
fmap f Nothing = ...
fmap f Just x = ...
```

Now, 

```haskell
fmap f Nothing = Nothing
```

Can we put something else than `Nothing`? Now, since Haskell is a lazy language, we could always put `bottom`. But besides this, why must it be `Nothing`? In this case, we don't have an `a`, and we don't have a `b`. We have a mental block as programmers here: we could not imagine anything else but `Nothing`, here. We could say "It's `Nothing` unless the type `a` is `Integer`. In that case, we will have `Just 0`". It's silly but possible. For all `a` is `Nothing` *except* for 1, where we use a different definition.

We want to use polymorphic functions: Haskell tells us that the function should be parametric and polymorphic. Here we are using parametric polymorphism. There is also something called ad-hoc polymorpism, which would allow us to define `fmap` in a different way for `Integers`. In Haskell we are somehow straying from pure mathematics, we are actually imposing a stronger condition than being a functor by imposing ourselves the rules or parametric polymorphism. It is much more restrictive, so much that it actually leads to the so called [Theorem for Free](https://bartoszmilewski.com/2014/09/22/parametricity-money-for-nothing-and-theorems-for-free/).

Parametric polymorphism means that a function will act on all types uniformly.

Indeed, for parametric polymorphism, `Nothing` is the only option.


For the second option, we could also define:

```haskell
fmap f Just a = Nothing
```

Would it be a good functor? Homework.

The obvious choice is:

```haskell
fmap f Just x = Just (f x)
```

So, in conclusion

```haskell
fmap f x = case x of
    Nothing -> Nothing
    Just a -> Just f a
```

or

```haskell
fmap f Nothing -> Nothing
fmap f Just a -> Just f a
```

Or, in free point style:

```haskell
fmap f = 
  \x -> case x of 
    Nothing -> Nothing
    Just a -> Just f a
```


### Conclusion
We defined a mapping of objects/types:

```haskell
data Maybe a = Nothing | Just a
```

and a mapping of functions/morphisms:

```haskell
fmap :: (a -> b) -> (Maybe a -> Maybe b)
```

But we still don't know if this is a Functor: is it mapping identity to identity? Does it preserve composition?

We must verify it.
