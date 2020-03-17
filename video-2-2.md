Monomorphisms, simple types
===========================

So, that's the definition of Epimorphism:

```haskel
f :: A -> B is an epimorphism if:

for every C
for every g1, g2 :: B -> C

if g1 . f = g2 . f => g1 = g2
```

Let's do the same for monomorphism

## Monomorphism
Let's start with something that is *not* a monomorphism (not an injective function)

```haskell
f :: A -> B

f a1 = b
f a2 = b
```

Let's use an object/set C before, so let's play with pre-composition:

```haskell
g1 :: C -> A
g2 :: C -> A

g1 c1 = a1
g2 c2 = a2

(g1 . f) c1 = b
(g2 . f) c2 = b
```

and yet `g1 != g2`.

```haskell
for every C
for every g1, g2 :: C -> A


if f . g1 = f . g2 => g1 .g2

then f is a monomorphism
```

## Isomorphism
In Set Theory, if a function is both injective and surjective, it is bijective (invertible).

Is this also true in Category Theory? Can we say that a morphism that is both an epimorphism and a monomorphism is an isomorphism? No.



## Sets
Let's go back to sets, since they are our model for Types.

### Empty Set
Is there an equivalent Type for the Empty Set?

Empty Set in Haskell corresponds to the Type `Void`. `Void` contains no element, and there is no way to construct it.

In fact, in Haskell types contains the Bottom element, so the Empty Set really is not empty. Bottom is used in Haskell to model functions that never terminate.

Can we define functions that take `Void` as arguments, that would go from `Void` to `Integer`? Mathematically speaking, yes, otherwise it would be impossible to define the identity for `Void`.


```haskell
idVoid :: Void -> Void
```

because every object in a Category *must* have an identity. This very function cannot be called (because we cannot provide it an argument), but it exists.

This function in Haskell has the name `absurd`:

```haskell
absurd :: Void -> a
```

In Logic this function corresponds to False. In Logic we cannot construct Falsity from something, that is, we cannot prove something that is false: something that's false is false, it has no proof.

## Proposition as types
Functions are proofs. In the correspondance between types and logic, called Propisition as types, the existence of a function corresponds to a proof. [Proposition as type](https://homepages.inf.ed.ac.uk/wadler/papers/propositions-as-types/propositions-as-types.pdf) links logic to computation. 

Since we cannot create an instance of `Void`, there is no proof of falsity.
 
On the other hand, if we assume falsity, from false follows anything. Here's why the definition 


```haskel
absurd :: Void -> a
```

From false premises we can derive anything.


## Singleton
After `Void`, which has no element, there's the Category with one single element, called Singleton (Singleton Set in Set Theory). In Haskell it's called Unit, and it's represented with `()`.

Unit has one single element. This single element can be constructed from nothing, from thin air, it just is. This element is also represented as `()`.

So, Unit is a type `()` which has a single element `()`. We can write:

```haskell
() :: ()
```

From the point of view of Logic, this corresponds to True. 

A function that takes anything and goes to Unit, regardless of its argument generates from thin air a Unit. This function is called `unit`:

```haskell
unit:: a -> ()
```

A function that takes a Unit and returns an int:

```haskell
f :: () -> int
```

This function must be constant, it must return always the same integer. There must be a lot of those functions: the function that generates `1`, the one that generates `2` and so on.

```haskell
one :: () -> 1
two :: () -> 2
```

There must be such function for any types:


```haskell
true :: () -> True
false :: () -> False
```

In general, there is one function for each possible value/element of a type.

So, we can say that the family of functions from Unit corresponds to picking elements of Sets. The define in some way elements of a Set or, we say, they generalize elements of an object. In fact, they are called *generalized elements*.

Therefore, we can replace talking about element with talking about morphisms.

Not all categories have singleton objects.


## 2 elements sets
A Set with 2 elements. This always correspond to the Boolean set. It can be defined as a Sum of generalized elements.

`Void` and `()` form the basis for the rest.

We can talk about functions returning bools, called predicates.
