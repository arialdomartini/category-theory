Monoidal categories, Functoriality of ADTs, Profunctors
=======================================================

In a monoidal category we want to define what does it mean to multiply 2 objects.

A categorical product is like a multiplication, we have one part of a monoid, because we have a binary operation. As we saw in  [video 3.1](video-3-1.md), in Set Theory a monoid is a set with some binary operator defined in it, with 2 conditions:

* it defines a *unit*, so that an element multiplied by the unit returns the element itself: `for each a there esist e such as e * a = a * e = a`
* associativity: `(a * b) * c = a * (b * c)

So far, talking about monoids we were in Set Theory. Now we want to talk about Categorical Monoids. Here the binary operation operates on objects, not elements of a set, or on morphisms.

We already have defined product. In order to be a monoid, we also need associativity and unit. Remember that the unit for multiplication in Haskell was the unit type `()`, which is the singleton set, so in general a terminal object. Let's see if this terminal object is a good candidate for being the unit in a categorical monoid.

If we construct a product: we have an object `a` and a terminal object `()`. `a * ()` would have 2 projections:

``` haskell
      a * ()
     /      \
    a        ()
```

If `()` is the unit, `a * ()` would be nothing else than `a` itself.


``` haskell
      a 
     / \
    a   ()
```

We need to prove that this is the best candidate. The projections are:

```haskell
      a 
   p / \ q
    a   ()
```

where `p = id`, and `q` is `unit`. `unit` is unique. 

```haskell
      a 
  id / \ unit
    a   ()
```

It's a good candidate. But, is it the best one? Let's try someother, `b`:


```haskell
      b
   p / \ unitB
    a   ()
```

We need to prove that there is a unique morphism from `b` to `a`. We already have this morphism represented in the diagram: it's `p`.


```haskell
       b
   p /p| \ unitB
    /  a  \
    \ / \/
     a   ()
```

And `id . p = p`. It must be unique, because no other morphism combined with `id` can give use `p`.
