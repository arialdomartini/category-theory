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



