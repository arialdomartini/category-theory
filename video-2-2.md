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

    
