Products
========

Again about Terminal Objects: we didn't say anything about outgoing arrows. There are usually outgoing arrows from Terminal Objects. These are the arrows that help us define the Generalized Elements: every arrow to an element can be used as the definition of the element.

Initial object and Opposite Category
====================================
We could just say, let's do the same already seen for Terminal Object, just reverse it. This trick is general. Every construction in category theory really has its opposite contruction, done by reversing arrows. This property is related to the fact that for every category we can always create another almost identical category in which all the arrows are reverted, the opposite category, so from `C` to `Copp`.

`C` might contain:

```haskell
f :: a -> b
g :: b -> c

g . f :: a -> c
```
plus the identities, while `Copp` whould contain:

```haskell
fopp :: b -> a
gopp :: c -> b

fopp . gopp = (g . f)opp :: c -> a
```

It's still a category.

Initial object is the Terminal object in the opposite category.


# Cartesian product
In terms of 2 sets `A` and `B` is the set of all the possible pairs of elements of `A` and elements of `B`.

The cartesian plan is one example, being `X` and `Y` real and the plan all the possible points given by the cartesian product of `X` and `Y`.

There are 2 special functions called projections, in Haskell `fst` and `snd`.

```haskell
P = A x B
snd P = a
snd P = b
```

We are not constrainted with numbers. `A` and `B` can be any category. That's again a pattern.

```haskell
fst :: (A x B) -> A
fst a x b = a

snd :: (A x B) -> B
snd a x b = b
```

In general, the pattern is: I have the objects `a`, `b` and `c`

```haskell
p :: c -> a
q :: c -> b
```

How to check if `c` is the cartesian product of `a` and `b`? We could have `c'` which is not, and still:

```haskell
p' :: c' -> a
q' :: c' -> b
```

Let's use Universal Construction again.

It there is a unique morphism `m :: c' -> c` and

```haskell
p . m = p'
q . m = q'
```

We say `p'` factorized into `p` times `m` (`p . m`), and `q'` factotized into `q .m`, so `p'` and `q'` have a common factor `m`. `m` factorizes the 2 projections `p'` and `q'`. They take the worst from them and condenses them in the real projections, getting to the same result. It's like `m` loosing some information (think about surjection and injection).

In Haskell

```haskell
fst (a, _) = a
snd (_, b) = b
```

Let's see with a bad projection. Let's take 2 functions that have the same signature of the projections of the type `(Int, Bool)`:

```haskell
c :: (Int, Bool)

p :: Int -> Int
q :: Int -> Bool
```

and let's see why
```haskell
c' :: Int
```

is not the cartesian product of `Int` and `Bool`.

For example:
```haskell
p = id
q = True
```

So,

```haskell
m :: Int -> (Int, Bool)
m x = (x, True)
```

This is non-surjective bad guy: it misses all the pairs `(x, False)`. It just covers a line in the cartesian plan.


Let's try with a candidate which is richer, for example a triple:

```haskell
c' :: (Int, Int, Bool)
p' :: (Int, Int, Bool) -> Int
q' :: (Int, Int, Bool) -> Bool

p' (x, _, _) = x
q' (_, _, y) = y
```

Now, `c'` is too big to be the cartesian product. It covers more than the cartesian plan, it covers a cube.

`m` maps from the bad candidate to the good candidate:


```haskell
m (x, y, w) -> (a, w)
```

`m` is not injective. Like in the previous example, this candidate has some "flaw": it's non-injective, the other one was non-surjective. We distilled the flaws into `m`. We can discuss it using epimorphisms and monomorhisms, not element. We could even avoid talking about cartesian product, and call it just product, or categorical product.


## Definition of categorical product
So, categorical product of `a` and `b` is a triple, an object `c` with 2 projections `p` and `q`

```haskell
p :: c -> a
q :: c -> b
```

with the universal property that for any other object `c'` with 2 projections `p'` and `q'` (for any other "pretender"), there is a unique morphism `m` such that factorizes the 2 projections:

```haskell
m :: c' => c
p' . m = p
q' . m = q
```

Not every category has product. Even if it has product, maybe it has not for every pair of object. In sets, products can be defined between any 2 object. In opposite category, we can have co-products, which we will talk about next time.


