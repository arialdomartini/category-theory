Functors in programming
=======================

So, we have defined a Functor:

``` haskell
data Maybe a = Just a | Nothing

fmap :: (a -> b) -> (Maybe a -> Maybe b)
fmap f Nothing = Nothing
fmap f Just x = Just f x
```

We defined both the mapping of objects and morphisms. We also have the Functor Laws:

* preserve composition
* preserve identity

Haskell compiler cannot check these conditions: in the type system we cannot encode these laws.

We want to prove that this Functor preserves identity, that is:

``` haskell
fmap id = id
```

(We should have written

``` haskell
fmap idA = idMaybeA
```

But since it's a polymorphic `id` we could just write `id`)

It should also preserve composition:

``` haskell
fmap (f . g) = (fmap f) . (fmap g)
```

Now, this is not valid Haskell: with the symbol `=` Haskell *defines* functions. Here, on the contrary, we would like to check equality.<br/>
In Haskell every definition of a function is an equality: it means the left side can be replaced with the right side, wherever it is found. This is called *inlining*: inlining is not always correct because of side-effects. With pure functions inlining is safe.

We can do the opposite of inlining, which is called *refactoring*: you find an expression somewhere and you lift it turning it into a function.

## Equational Reasoning
We can use Equational Reasoning (enabled by referential transparency and being able to replace equals by equals in all contexts), which works by inlining definitions.

Let's do it with:

``` haskell
fmap id = id
```

`fmap id` produces a function that goes from `Maybe a` to `Maybe b`. So, we have to evaluate the 2 cases, `Just a` and `Nothing`.

## Nothing

``` haskell
fmap id Nothing = ???
```

Let's see the definition:


``` haskell
data Maybe a = Just a | Nothing

fmap :: (a -> b) -> (Maybe a -> Maybe b)
fmap f Nothing = Nothing
fmap f Just x = Just f x
```

Therefore:

``` haskell
fmap id Nothing = Nothing
```

Let's see also the definition of `id`:

``` haskell
id x = x
```

So

``` haskell
id Nothing = Nothing
```

This means we can replace `Nothing` with `id Nothing` everywhere we wish (we are applying *refactoring*):

``` haskell
fmap id Nothing = Nothing
fmap id Nothing = id Nothing
```

Let's see the other case.

## Just x

``` haskell
fmap id Just x = ???
```

Again, let's take the definition:


``` haskell
data Maybe a = Just a | Nothing

fmap :: (a -> b) -> (Maybe a -> Maybe b)
fmap f Nothing = Nothing
fmap f Just x = Just f x
```

From this it follows:

``` haskell
fmap id Just x = Just id x = Just x
```

Again, if we take the definition of identity, and we apply refactoring:

``` haskell
id Just x = Just x
```

it follows

``` haskell
fmap id Just x = id Just x
```

## Conclusion
So

``` haskell
fmap id Nothing = id Nothing
fmap id Just x = id Just x
```

Then:

``` haskell
fmap id = id
```
We could apply Equational Reasoning to the second Functor Law too:

``` haskell
fmap (f . g) = (fmap f) . (fmap g)
```

but here we won't.
