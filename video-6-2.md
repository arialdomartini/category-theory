Functors in programming
=======================

## Verifying Functor Laws for Maybe
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

### Equational Reasoning
We can use Equational Reasoning (enabled by referential transparency and being able to replace equals by equals in all contexts), which works by inlining definitions.

Let's do it with:

``` haskell
fmap id = id
```

`fmap id` produces a function that goes from `Maybe a` to `Maybe b`. So, we have to evaluate the 2 cases, `Just a` and `Nothing`.

### Nothing

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

### Just x

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

### Conclusion
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

but here we won't. Besides, we don't even need to. Since we are using Parametric Polymorphism, this would become Theorem For Free. This means that it is enough to proove for `id`, and from it it follows the proo for `f . g`.

Monads have their laws, and we will need to demonstrate them too.


## Defining new Functors
In general, in Haskell, when we define a new Functor (that is, we define the data type and the `fmap` function), we wish to know if it really is a Functor. In general, everything we do with Algebraic Datatype is automatically a Functor.

Let's see what *lifting* means. We have

``` haskell
f :: a -> b
```

If we have the functor `Maybe`, 

* `a` is lifted to `Maybe a`
* `b` is lifted to `Maybe b`
* `f :: a -> b` is lifted to `Maybe f :: Maybe a -> Maybe b`


* Lifting* refers to this image of moving stuff to a higher dimension. `fmap` is a *higher order polymorphic function*.
* it's a *higher order* because it takes a function and returns a function
* it's polymorphic because it takes functions `f :: a -> b` and `a` and `b` are arbitrary.

### ad-hoc polymorphism and type classes

For each different Functor, we define a different `fmap` implementation. We cannot write one single `fmap` for every Functors. We see here a different kind of polymorphism: one is on the type of the function, and one on the kind of Functor. The latter is called *ad-hoc* polymorphism. In Haskell we have both. We just use different tools for those different types of polymorphisms. For *ad-hoc* we use *type classes*. With type classes we defined a family of types (or class of types) that share some kind of interface. This is somehow similar to object oriented programming languages.

For example, we can have

``` haskell
class Eq a where
  (==) :: a -> a -> Bool
```

This class defines the family `Eq` of every type that supports this kind of operator. The implementation of `==` will be different for each type. That's *ad-hoc* polymorphism which is parametrized by the type.

But the Functor itself is parametrized on a type: `Maybe a` takes a parameter that is a type. So, `Maybe a` is not a type: it's a *type constructor*. Fortunately, in Haskell, type classes work not only for types, but also for type constructors.

If we want to define Functor (not *a* Functor like `Maybe`, but `Functor` as the concept), we need to define:

``` haskell
class Functor f where
    ...
```

Note that `f` is lowercase, because it's a type parameter: in this case, it's a *type constructor* parameter. We don't need to specify if `f` is a type or a type constructor. There are ways to specify this, but we are not forced, because the next line will let the compiler infer it:

``` haskell
class Functor f where
    fmap :: (a -> b) -> (f a -> f a)
```

and here the compiler figures out that `f` operates on `a`, that is, on a type, so `f` is a type constructor.


### Some examples
`Maybe` is an example of Functor. There are many other examples, each very different from the others, so that it's not simple to get the general idea of functors only by viewing them. We could just say the a Functor is any type constructor that support `fmap` (plus, `fmap` itself).

#### List
The most intuitive example for Functor is List. Lists are already defined in Haskell, but we are going to redefined it.

List can be defined as a coproduct:

``` haskell
List a = Nil | Cons a (List a)
```

`List` is a type constrcutor: it takes an arbitrary type `a` and constructs a type (List of Int etc).

Let's define `fmap` for it, to make it an instance of `Functor`:

``` haskell
instance Functor List where
    fmap ....
```

In this case, `fmap` would take a function from `a -> b` and would produce a function from `List a -> List b`. Since `List` is a coproduct, we have 2 cases here: `Nil` and `Cons a (List a)`.

``` haskell
instance Functor List where
    fmap f Nil = Nil
    ...
```

Since we don't use `f` we could write

``` haskell
instance Functor List where
    fmap _ Nil = Nil
    ...
```

Now for 

``` haskell
instance Functor List where
    fmap _ Nil = Nil
    fmap f (Cons h t) = ...
```

where `h` (head) is of type `a`, and `t` (tail) is of type `List a`.

``` haskell
instance Functor List where
    fmap _ Nil = Nil
    fmap f (Cons h t) = Cons (f h) (fmap f t)
```

#### Reader
In infix notation:

``` haskell
type Reader r a = r -> a
```
or in prefix notation:

``` haskell
type Reader r a = (->) r a
```

So, `Reader` is a type constructor that takes 2 types `r` and `a` and produces a types of function from `r` to `a`.

Using partial application, `Reader r` is the Functor that associate `a`  to `r -> a`. For example, the Functor `Reader Bool` would associate the type `Int` to type `Bool -> Int` (which is a function). `(->) r` is a type constructor. Let's define `fmap`. What's its type?

Remembering that:
``` haskell
fmap :: (a -> b) -> (F a -> F b)
```

since here `F a = Reader r a = r -> a` we have:

```haskell
fmap :: (a -> b) -> (r -> a) -> (r -> b)
```

Let's see the implementation of `fmap` for `Reader r`. We have to play to Type Tetris, to match types:

``` haskell
fmap f Reader a =
fmap f g = \r -> f (g r)
fmap f g = f . g = (.) f g
fmap = (.)
```

