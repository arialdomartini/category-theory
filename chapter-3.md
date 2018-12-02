Categories Great and Small
==========================

## Category with no objects

In a category with no objects there are no morphisms. It is a useless category, per se, but it makes sense when defining more complex concepts, just like empty sets in set theory.

## Free Categories and Quivers

A Free Category is the category that results from freely adding morphisms between the nodes of a Quiver or a Directed Graph, ending up with an infinite number of morphisms (since they include all the possible combination of simpler morphisms) (see [Free Category](https://en.wikipedia.org/wiki/Free_category)).

    If Q is the quiver with one vertex and one edge f from that object to itself, then the free category on Q has as arrows 1, f, f∘f,f∘f∘f, etc.
    Let Q be the quiver with two vertices a, b and two edges e, f from a to b and b to a, respectively. Then the free category on Q has two identity arrows and an arrow for every finite sequence of alternating es and fs, including: e, f, e∘f, f∘e, f∘e∘f, e∘f∘e, etc.
    If a quiver Q has only one vertex, then the free category on Q has only one object, and corresponds to the free monoid on the edges of Q.
    
## Orders

Before talking of Categories with one single object (Monoids) let's talk about Orders and hom-sets.

### Preorders (or Quasiorders)

In mathematics a preorder or quasiorder is a binary relation that is reflexive and transitive. An example of preorders is the reachibility relationship in a graph.<br/>
We often use the symbol ⩽, but this is somehow confusing because it does not correspond to the mathematical symbol.

Let's take a category where the morphism represents the relation of being *less than* or *equal to*.

* The Identity morphism exists, because every object is equal to itself;
* There's composition, because if a ⩽ b and b ⩽ c then a ⩽ c;
* Composition is associative, because if (a ⩽ b) ⩽ c then a ⩽ (b ⩽ c) ???

In a pre-order there can be cycles.

### Partial Order (Poset)
It is a Preorder with the additional condition that, if a ⩽ b and b ⩽ a then a == b.

```haskell
if a <= b and b <= a then a = b
```

An example is the relation `⩽` in the set of real-numbers.

## Total Order
It's an order where any 2 objects are somehow in a relationship, no one excluded.

## Hom-sets
The set of morphism from object `a` and object `b` in a category `C` is called *hom-set* and it written `C(a, b)` or `HomC(a, b)`

Applied to orders:

* Every hom-set in a preorder is either empty or a singleton:
  * `C(a, a)` is a singleton
  * `C(a, b)` can be empty, or a singleton
* In a Partial Object every hom-set is either empty or a singleton:
  * There are no cycles, then if there is a morphism from `x` to `y` and a morphism from `y` to `x` (which by the above implies that `x` and `y` are isomorphic), then `x=y` (see [ncatlab](https://ncatlab.org/nlab/show/partial+order#AsACategoryWithExtraProperties))
* In a Total order all the hom-sets are singleton
  * Since all objects are in a relationship, `C(a, b)` is a singleton for every couple of objects

## Monoids

    * In Set Theory:
        * In Set Theory, a Monoid is a Set with a binary, associative operation
            * A Monoid is an algebraic structure 
                * with a single associative binary operation 
                * and an identity element. (Wikipedia)
        * Examples
            * natural numbers form a Monoid under addition
                * it is associative
                ```haskell
                  (a + b) + c = a + (b + c)
                ```
                * The identity (the neutral element) is 0
                ```haskell
                  a + 0 = a
                ```
        * In Haskell
        ```haskell
        class Monoid m where
            mempty :: m
            mappend :: m -> m -> m
        ```
            * `mempty` defines the identity  (or the neutral) element
            * `mappend` is the binary function
    * In Categoty Theory
        * A monoid is a a Category

        * We could replace elements of the set (natural numbers) with functions
            * add3, the function that adds 3, and so on
                * such functions associate an element m to a function m -> m
                * this reminds of the type of 
                ```haskell
                    mappend :: m -> m -> m
                ```
                which we could reformulate as
                ```haskell
                    mappend :: m-> (m -> m)
                ```
                to highlight that they associate numbers to adder functions
        * It's a Category with a single object
        * Is it always true that a categorical monoid defines a unique set-monoid, that is a set with binary, associative operation with an identity element?. That is, can we always recover a set monoid from a categorical monoid?
            * Yes. 
                * Consider the hom-set `M(m, m)` of a categorical monoid `M`.
                    * in our examples, they are the adders (`add3`, `add50`, `add0`)
                * take two morphisms `f` and `g` from that set
                * they can always be composed
                * the identity element exists, since it is `add0`
                * Therefore, we can always define a binary operation in that set, as the product of two element in the set (that is, the composition of the morphisms in the category world)
                ![Relation between categorical monoid and its hom-set](monoidhomset.jpg)

            
