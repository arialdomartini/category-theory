Algebraic data types
====================

## Product of types compared to product in monoids

Why is it an algebra. We have product and sum. Product is sort of multiplication: it's a monoid. A monoid is something that has a multiplication which is associative. Is there anything like an algebra of types?

Let's check a few things, using Haskell. Product of number is symmetric. Is it symmetric for types? No, it's not. A pair `(Int, Bool)` is not at all equivalent to a `(Bool, Int)`. It won't typecheck. Yet, they contain the same information: they are isomorphic. And the isomorphisms between them is `swap`:

```haskell
swap :: (a, b) -> (b, a)
swap p = (snd p, fst p)
```

or

```haskell
swap (a, b) = (b, a)
```

So, product of types is not symmetric really, but it is symmetric up to an isomorphism.

### Is it associative

Is it associative? Is the following valid?

```haskell
((a, b), c) = (a, (b, c))
```

No! But, yet, they contain the same information, they are isomorphic (`((a, b), c) ~ (a, (b,c))`). Let's look for an isomorphism:

```haskell
assoc :: ((a, b), c) -> (a, (b,c))
assoc p = (fst fst p, (snd fst p, snd p)
```

or, using Pattern Matching:

```haskell
assoc ((a,b),c) = (a, (b,c))
```

`assoc` and `swap` are isomorphisms.

### Does it have a unit?
Does it have a unit of multiplication? That is, what would be the type that if you pair it with any other type, you get the same type back?

```haskell
(a, u) = a
```

It must be a type with one single element, otherwise I would be multiplying the number of results. It's `()`, up to `fst`

```haskell
(a, ()) ~ a
```

`(a, ())` is isomorphic to `a`, and the isomorphism is `munit`.

```haskell
munit (a, ()) = fst (a, ()) = a
munit-inverse a = (a, ())
```

This is like building the cartesian product of a vertical line with a single element on `x`: you would get the same line, shifted right of `x`.

This in `(a, ())` is right unit. But we know multiplication is symmetric up to an isomorphism (swap), so we know this is also valid for right unit.

So, this is a monoid.

## Multiplication
We could really write

```haskell
(a, ()) ~ a  is equivalent to a * 1 = a
```

Then, the standard expressions stands, like `a * (b * c) = (a * b) * c`.

Since it's associative, this means we can skip using parenthesis:

```haskell
(a, (b, c)) ~ (a, b, c)
```

What about Sum (or coproduct)


## Sum
It is symmetric up to isomorphism

```haskell
Either a b ~ Either b a
```

It is also associative, up to isomorphism, and we could define:

```haskell
data Triple a b c = Left a | Middle b | Right c
```

This follows from the fact that the sum is associative.

What's the unit of sum? It's `Void`.

```haskell
Either a Void ~ a
```

`Void` is like 0, and `Either` is like `+`.

In `Either a Void` I could construct a right if you provide me with an element of `Void`. But this won't happen. `Either a Void ~ a` is equivalent to `a + 0 = a`.

### Other examples
We know that `a * 0 = 0`. In category, `(a, Void) ~ Void`. Yes, because, in order to build `(a, Void)` I'd need an element of `a` and an element of `Void`. So, that set is empty, it's `Void`.


Let's see distributive law:

```haskell
a * (b + c) = a * b + a * c
```

would be

```haskell
(a, Either b c) ~ Either (a, b) (a, c)
```

## Algebraic data types
What is a structure called when there is both a multiplication and a sum? It's a Ring. Except that a true Ring should also have the inverse of Sum, which here we don't have: there's no inverse of an Integer. A Ring without inverse is called Rig (without the n for negative) or semiring.



### 1 + 1 = 2

```haskell
1 + 1 = 2
```

would be equivalent to 

```haskell
Either () () = Bool
```


### 1 + a
```haskell
1 + a
```

is the `Maybe` type, or `Either () a`

```haskell
Maybe a = () | Just a
```

usually defined as

```haskell
Maybe a = Nothing | Just a
```

`Nothing` is just like a `Left ()`.


### Solving equations
```haskell
f(a) = 1 + a * f(a)
f(a) - a * f(a) = 1
f(a) * (1 - a)  = 1
f(a) = 1 / (1 - a)
```

Let's transate it into types:

```haskell
f(a) = 1 + a * f(a)
data List a = Nil | Cons (a, List a)
```

It's a linked list!

Unfortunately, we cannot express `f(a) = 1 / (1 - a)` with a list. But we could notice that:

```haskell
f(a) = 1 / (1-a)
```

is the value a geometric sequence converges to.

```haskell
Sum n = 0 -> infinity = a^n = 1 + a + a^2 + a^3 + ... = 1 / (1 - a)
```

`1` is an empty list, `a` is the singleton list etc.

```haskell
data List a = Nil | Cons (a, List a)
```

can be solved by substitution (expansion). Let's start before with:

```haskell
f(a) = 1 + a*f(a)
f(a) = 1 + a*(1 + a*f(a))
f(a) = 1 + a + a^2*f(a)
f(a) = 1 + a + a^2*(1 + a*f(a))
f(a) = 1 + a + a^2* + a^3*f(a)
...
```

With Haskell, it would be:

```haskell
data List a = Nil | Cons (a, List a)
data List a = Nil | Cons (a, Nil | Cons (a, List a))
```

This is a way of resolving the geometrical sequence, with substitution. This can be formalized in the [Fixed Point combinator](https://en.wikipedia.org/wiki/Fixed-point_combinator).
