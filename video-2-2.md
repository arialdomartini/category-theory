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
