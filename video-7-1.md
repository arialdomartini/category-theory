Functoriality, bifunctors
=========================

## Functors and Endofunctors
So we saw that

* Functors are mapping *between* categories
* Endofunctors are mapping *within* a category

The rules are just the same.

A Functor is like a number of functions put together.

* There is one major function that map objects (and this is an actual function only if the category is small, that is, only if its objects form a set)
* But it also has to preserve the structure of category, hence Functor maps the connections between objects, the morphisms: for each pair of objects we have the set of morphisms, the hom-set, and we define a mapping between hom-sets to the corresponding hom-sets in the othere category, and the mapping is a function.

We also saw that Functors must preserve the categorical structure, that is identity and composition.

## Functor composition

Now, since Functors are built from functions, we know that functions compose. Maybe we can compose functors.

Say we have a functor `F` from category `C` to `D` and one `G` from `D` to `E`. We can think of a functor which is the composition of `F` and `G`.

Object `a` would be mapped through `F` as `F a` and through `G` in `E` as `G(F a)`. Also morphisms would be. For example, `f :: a -> b` would be mapped into `D` with `F` as `F f`, and into `E` with `G` as `G (F) f`. We are not doing nothing special: this is just function compositions. `F` is a function on objects, `fmap` is a function on hom-sets: after all, they are just functions.

### Identity Functor
Since we have composition of functors, it's legit to ask if there is identity. It must be a functor that maps object on themselves, and each morphisms to itself, without changing anything. This identity functor is of course an endofunctor. It must obey 

```haskell
id . F = F
F . id = F
```

### Cat
Whatever we learn on functions, we can apply to functors.

So, it's a category! It's a category in which objects are categories, and morphisms are functors. This category is called *Cat*.

There are some subtle details. We know that categories can be small or large (see [Chapter 3 - Categories Great and Small](chapter-3.md)), and things can become a bit complicated. In case we have a category of large categories, we have to use a more powerful tool: we will get to it later.

#### Example
Let's try to compose 2 functors in programming: `Maybe` and `List`. Let's consider the function `tail :: [a] -> [a]` which returns the tail of a list, throwing away the head of a list. This function is defined only for non-empty lists. If the list is not empty, the program dies. That's bad, especially because this function is in the core library.

To be safer, let's define:

``` haskell
safeTail :: [a] -> Maybe [a]
safeTail [] = Nothing
safeTail (x : xs) = Just xs
```

`Maybe List a` is also a Functor. Let's say we want to apply square to the value of items in `Maybe List Int`: we could of course define a function, like we have just done with `safeTail`, but it's a pity: we already have `fmap` for `Maybe` and `fmap` for `List`.

``` haskell
square :: Int -> Int
square x = x * x * x
```

We want to apply this function to some Maybe list `mis :: Maybe [Int]`. We need to apply something `??` to `mis`.

``` haskell
fmap ?? mis
```

Now, this function `??` must be an `fmap` itself, because it must operate on `[Int]`:

``` haskell
fmap (fmap square) mis
```

In other words, we need to jump 2 layers of functors. We can write it as:

``` haskell
(fmap . fmap) square mis
```

### Algebraic Datatypes
Most type constructors that we normally use in Haskell are automatically functorial, or not too hard to make functorial. Data structures that are alebraic are automatically functorial: algebraic data structrures are formed with sums and products.

We want to show now that if we create an algebraic data type using these operations then we automatically have a functor. 

The first question is: is product of 2 types a functor?

#### Product of categories
A product is a tuple `(a, b)`. This can be written as a type constructor, as a sort of infix notation `(,) a b`. If we fix `a`, this is a type costructor in `b`.

Now, what does it mean to apply (map) a function to it?

``` haskell
        fmap f
(e, a)   -->  (e, b)
  ^             ^
  |             |
  a      -->    b
          f
          
          
fmap f :: (a -> b) -> (e, a) -> (e, b)
fmap f (e, x) = (e, f x)
```

Again, we can think of a pair as a container, that contains the second element on which we apply the function `f`.

We could invert the items and say that the pair is functorial on the first item. Is it functorial on the same 2 arguments at the same time? Can we generalize the idea of Functor and have a Functor on 2 arguments?

Indeed we can do this, exept we don't really have to. In Haskell we do, but in Category Theory we can play with categories with another trick. We can define a Functor that acts on a pair of categories, and takes one element from a category and the other from another category; here with Haskell, `a` and `b` are both from the same category, but in general they don't have to. We can define a product of 2 categories, just like we do with functions: after all, a function of 2 arguments is isomorphic to a function of 1 single argument which is a pair (a cartesian product).

It turns out that this is simple to do, at leaset for small categories: in small categories, objects form a set, so we can costruct a product category like we constructed cartesian products. If we have 2 categories `C` and `D`, `C*D` is the category whose objects are pairs of objects `(c, d)` for each `c` in `C` and each `d` in `D`.

What about the morphisms?

Say we have a morphisms `f :: c -> c'` and `g :: d -> d'`. In `C*D` we have a pair `(c', d')` and a *pair* of morphisms `(f, g)`.

Composition would be like:

``` haskell
(f', g') . (f, g) = (f' . f, g' . g)
```

Identity would be `(id, id)`, with the first in `C` and the second in `D`.

Once we have defined the product, we can define a Functor from `C*D -> E`: this would map *pairs* of objects from `C*D` to objects in `E`, and each *pair* of morphisms in `C*D` to a morphism in `E`.

This is called a *bifunctor*.

If we want to do this in Haskell we have to lift a morphism from a product category. Since we are in Haskell, this would be the product of a category with itself: `C * C -> C`, where `C` is the category of types and functions. Yet, this would not be the functor from set to set, or to Hask to Hask, but from a product of 2 Hasks. We are already getting outside of Hask and we are getting into Hask square.

This is a mapping from 2 types to a type, which resembles what we wrote before with `(,) a b`, which produces a tuple.

We are also lifting 2 functions at the same time. So, if we want to define a bi-functor in Haskell, we would have:

``` haskell
class Bifunctor b where
  bimap :: (a -> a') -> (b -> b') -> (f a b -> f a' b')
```

The compiler figures out that `f` is a type constructor that takes 2 types as arguments.

Something that is a bifunctor is automatically functorial in the first argument: you fix the first argument, and it's functorial on the second one, and you can get it by putting an identity in one of the arguments, getting one of the 2 `fmap`s.

#### Sum
What about sum of 2 categories? We don't need to get through it. We can use the same bifunctor idea:

`Either a b` is actually a bifunctor: we can define the action of 2 function on `Either a b`: `Either a b` is a type constructor that takes a pair of types and produces a type.

A category for which a product is defined for every pair of objects is called Cartesian Category. In a Cartesian Category, then Product is a Bifunctor. The same is true for Coproduct, because it takes 2 types and produces a 3<sup>rd</sup> one.

##### Products of morphisms

Say we have `a*b` and 2 projections `p` and `q` to `a` and `b`, and we also have:

``` haskell
f :: a -> a'
g :: b -> b'


        a*b
     p /   \ q
      /     \
     /       \
    /         \
   a           b
   |           | 
 f |           | g
   a'          b'
```

We know we can build a product from `a'` and `b'`.


``` haskell


        a*b
     p / | \ q
      /  |  \
     /   |   \
    /    |??  \
   a     |     b
   |   a'*b'   |
   | p'/   \q' |
 f |  /     \  | g
   a'          b'

```

If we want to show that this is a Bifunctor we need to show that we can lift `f` and `g` to something that goes from `a * b` to `a' * b'`, which we showed as `??`.

In Haskell we just applied `f` and `g` to each argument. In general, we would need to apply the definition of product: for any other candidate, there is a unique morphism from that candidate to the actual thing. We just need to think to `a*b` as that candidate. From `a*b` to `a'` there is `f . p`, and to `b'` there is `g . q`. By definition `a' * b'` is the product, so there is a unique morphism from `a * b` to `a' * b'`, which we call `f * g`, the product of 2 functions.

