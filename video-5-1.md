Coproducts, sum types
=====================

Let's review Costruction of product, before delving with its dual, by reversing arrows and building the coproduct. It's a common topic in Category Theory: we will see Monads and Comonads, Monoids and Comonoids, Limit and Colimit and so on. So, maybe Initial object should have been called Coterminal Object.

Definition of product: a product between `a` and `b` is an object `c` with 2 morphisms `p` and `q` with `p : c -> a` and `q : c -> b`. There are a lot of objects with morphisms to `a` and `b`, but `c` is "the best one" because if we take any other `c'` which also has projections `p'` and `q'` there is a *unique* mapping `m` which will make the triangle 'c' -> c -> a' commute.

## Coproduct
Now, let's reverse the arrows:

```haskell
a    b
\   /
i\ /j
  c

i : a -> c
j : b -> c
```

`p` and `q` would be called *injections* instead of *projections*.

Let's try to find the "best" Coproduct, by reversing the arrows of the Product example.

```haskell
i' : a -> c'
j' : a -> c'

m : c -> c'

i' = m . i
j' = m . j
```

`c'` is the false coproduct, and `m` is unique.

Note from `p' = p . m` and `i' = m . i` that not only we do reverse the arrows, we also reverse the compositions.

We know that a product is in programming: it's a cartesian product, a pair. What a coproduct is in programming? It's a Sum Type.

The fact that we have the injections `i` and `j` means that we are embedding the set `a` in `c` and the set `b` in `c`. Since this is a universal construction, we want this injection to inject the whole thing. So, `c` is a set that contains both `a` and `b`, with no missing information and no extra information. All other `c'` would miss some information or would have some extra elements. `c` would define the ideal sum of `a` and `b`.

The question is what happens when `a` and `b` overlap, for example if `a = b`. Ideally, we could tag each element (this comes from the left, this from the right). That would be a discriminated union.

```haskell
c = (aLeft | aRight)
```

In this case, `m` would map from `aLeft | aRight` to `a`, and it would be non injective, because 2 different elements (one from the left and one from the right) would be mapped to the same element `a`.
