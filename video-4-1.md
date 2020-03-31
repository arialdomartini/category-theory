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


## Singleton Set / Terminal Object
We see a dualism between Set Theory and Category Theory: only, in the latter we never talk about elements.<br/>
We know in Set Theory there is the concept of Empty Set, a set without any element. How can we define the equivalent in Category Theory if we are not allowed to talk about elements? Or Cartesian Product. which in Set Theory is defined as the Set of the pairs of elements, if we cannot deal with elements?

All these concepts has to be redefined, or re-discovered in terms of morphisms and composition.

We use Universal Construction. The definition of Universal Construction and [Universal Property](https://en.wikipedia.org/wiki/Universal_property#) is very forman, and we won't cover it here. Let's talk about it only intuitively. We look for patterns (in terms of objects and morphisms) which are valid in a category.

There is an arrow from any sets to the Singleton Set (unit). From any type/set there is a function to unit, and the function is called unit. It's a function that just ignores its argument and cretes a unit.

```haskell

fa :: A -> ()
fb :: B -> ()
```

There is even a function frm the Empty set/Void to `()`. This is a sort of Universal Property of the singleton set: there's an incoming arrow from any other objects in the category. Does it really single out the Singleton Object? Is there any other type with the same property? Unfortunately, yes.

The Set category is very rich in arrows. There's almost a function for any sets. There's only one case in which there is no arrow: the arrows from a non-empty set to Void; there can be no arrow, because a function is a mapping between elements.

For the object representing `Bool` there are at least 2 morphisms incoming into it: `true` and `false`, which just ignore their arguments; but there can be more than 2 morphisms.

The singleton, on the contrary, only has 1 single arrow from another object. That's a possible definition of the Singleton object: it is a *Terminal Object*. This can be defined in any category. Not every category has a Terminal Object. It has a unique arrow coming from any other objects in the Category.

It must satisfy 2 conditions

```haskell
for each a in C there exists f :: a -> ()
```
(each object has a morphism to it)

and

```haskell
for each f,g :: a -> ()  => f = g
```
(and that morphism must be unique).


### Terminal object in Orders
In an order, it would mean that every object `a` is `lessOrEqual` of `()`. So, `()` would be the largest object. Not every ordered set has a largest object. Think of Natural Numbers, for example.


## Empty set / Void / Initial Object
Let's invert the arrows, and define the Empty Set as the object with only unique outgoing arrows to any other object.

```haskell
for each a in C there exist f :: Void -> a
for each f, g :: Void -> a => f = g
```

The function to Void is the absurd function. We have just inverted the definition for singleton set/terminal object. In Set Category this corresponds to empty set.


### Category with Initial and Final objects
In any category with a final object, because of composition and associativiry we can replace any path from `a -> b -> c -> ..... -> ()` with a single arrow `a -> ()`, no matter what path we take, it can be shrunk to `()`.

## How many terminal/initial?

The next questio that we might ask is how many terminal/initial objects can we have? 

If I have 2 terminal objects, are they equal? What does it mean for them to be equal? In category there is equality of arrows, but no equality of objects. We don't compare objects. We can instead asked if they are isomorphic.
```haskell
f :: a -> b
g :: b -> a

g . f = id
```

Terminal objects are equal up to isomorphism. And there is a unique isomorphism between them. Between 2 bool (true/false and black/white) there exist 2 different isomorphisms.

Let's take 2 terminal objects `a` and `b`. If `a` is terminal, there exist 1 and only 1 `f :: b -> a`.  But also `b` is terminal, so there exist 1 and only 1 `g :: a -> a`. From `a` there is also `ida :: a -> a`. If we now consider `g . f`, it's `g . g :: a -> a`. Since `a` is a terminal object, there must be 1 and only 1 arrow from any object (`a` included) to `a`, so `g . f = ida`, then `f` is an isomorphism. `a` and `b` are unique up to an isomorphism.

How does this relate to Universal Contruction? Follows a not-so-convincing argument.
