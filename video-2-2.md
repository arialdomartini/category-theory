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
