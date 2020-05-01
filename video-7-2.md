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

And `id . p = p`. It must be unique, because no other morphism combined with `id` can give use `p`. Indeed, multiplying by terminal object gives back the original object. So, we have the unity.

Of course, remember that in Haskell `a * ()` is not really equal to `a`, but it is equal up to a unique isomorphism: `(a, ()) ~ a`.

When we have categorical product and a terminal object, then we say we have a monoidal structure. The same happens with co-product and initial object, which is also a monoidal category. In general, we need a binary operation that is a bifunctor (and we know that both product and co-product are bifunctors), and we need a unit, then we get a monoidal category. Of course, we need also associativity (up to isomorphism).

We say that a monoidal category is a Tensor Product `*` and a unit `1`.

## Haskell
So far we saw that product and co-product are functorial. Sometime we construct data types that don't depend on a type argument: for example, `Bool = True | False`, does not take any type as argument, and it's not functorial. But we can tweak it a little bit and say it depends on a type, but not in a trivial way, which we call a *Const Functor*. Let's talk before a *Constant Functor*

### Constant Functor
A Constant Functor takes objects from a category and maps them to a single object of another category. It's like a black hole that takes anything and collapses it into a single object.

In Haskell this would be

``` haskell
data Const c a = Const c
```

(note that on the left we are defining `Const c a` which is a Type Constructor, and on the right `Const c` which is a Data Constructor. In Haskell we reuse and overload names not to confuse people, on the contrary, to avoid multiple, confusing names).

What happens to `a` in `Const c a`? It is just ignored.

Is this a Functor?

``` haskell
instance Functor (Const c) where
--  fmap :: (a -> b) -> (Const c a -> Const c b)
    fmap f (Const c a)
```

Note that here `Const c` is `Const c a` partially applied, the type constructor, not the Data Constructor.

