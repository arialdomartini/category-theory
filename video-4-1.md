Terminal and Initial objects
============================

## Kleisli category again
Let's recapitulate on Kleisli category, which is not so simple to grasp, as it requires to think about 2 categories at one time. 

We start from a category `A` containing `a`, `b` and `a->b`. We build a category `K` whose objects are just the same of `A`: `a` and `b`. However, the arrows are not the same: `a->b` in `K` is not the same `a->b` in `A`.

For every object in `A` we have some other object: we saw the specific case where for each type `T` we had a `Pair(T, string)` which is a diffrerent type, but still a mapping type based on `T`. Let's call the new type `m T`. It's a Functor, which maps a type to another type.

So, for a type `b` in `A` we have the type `m b`. So, in `A` we have the function `a -> b` and also `a -> m b` (in our case, `a -> (b, string)`. This is like the embellish arrow. The arrow `a -> (b, string)` is represented as `a -> b` in the Kleisli category.

It is a bit like we are implementing a new category in terms of another one.

### How do we know that the Kleisli category a category?
What would an arrow from `b` to `c` be in the Kleisli category?

Suppose we have in `A`: `a`, `b` and `c` with the morphisms

```haskell
f :: a -> b
g :: b -> c
```

The composition is `g . f`.

`b -> c` in `K` would be `b -> (c, string)` in `A`, so we have in `A`:

```haskell
f  :: a -> b
f' :: a -> m b

g  :: b -> c
g' :: b -> m c
```

In `A` `f'` and `g'` do not compose. In `K` they correspond to `a -> b -> c`, so they should compose. We saw the specific example with `m a` being `(a string)`, where we return `(c, string1 ++ string2)`, but does it work in general? No, it does not.

The identity in `K`: `ida : a -> a` in `K` would be `a -> m a` in `A`.

If we demonstrate that the Kleisli category is in fact a category (identity, composition, associativity), then the mapping `m` from `a` to `m a` and from `f :: a -> b` to `f' :: a -> m b` is called *monad*. This is one of the definitions of monad.



