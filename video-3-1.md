Example of categories, orders and monoids
=========================================

In the last videos we tried to reformulate some of the properties of sets in terms of morphisms.

## Empty Category
Let's start from the simplest possible category: the Empty Category, called Zero, `0`, not to be confused with the number `0`. It's a category with no objects.

It's useless, per se, but it's useful in context, just like the number 0. The context for this category is the category of all categories, for example for inductive proofs.

## Category with 1 object
It has at least 1 arrow, because each object must have the Identity morphism.

## In general: Free Construction
In general, we can start with a graph. Not every graph is a category. What's the connection between graphs and categories? We can start with a graph and continue adding arrows to it: for every node, we can add an identity arrow. Then, applying composition, for every pair of composable arrows in a graph, we should add the arrow representing the composition.

This kind of construction is called Free Construction, because we are not adding any constraints other than composition.

# Orders
An Order is an interest category, because its arrows are not functions: an arrow represents a relation, for example the relation `<=`, *less or equal than*.

`a -> b` means `a <= b` or `a` comes before `b`.

There are different kinds of orders:

* preorders
* partial orders
* total orders

We are used with total orders.

## Preorder
The simplest orders is the pre-orders: it's a relation that satisfies the minimun of conditions, the composibility

```haskell
a -> b and b -> c => a -> c
```

or

```haskell
a <= b and b <= c  => a <= c
```

In a total order, between 2 arbitrary objects, there must be an arrow. In a preorder, 2 objects can have no arrow (they can be not in relation).

In order to be a category, the relation `<=` must be reflexive (`a <= a`) and associative.

In general, in a category we can have multiple arrows between a pair of objects. In a preorder we have 0 or 1 arrow.

In principle, in a category we can have arrows in 2 directions (`a -> b` and `b -> a`), but in this case we cannot.

A category with these characteristics is called a *thin category* or *posetal category* (a category whose homsets each contain at most 1 morphism). *Posetal* comes from *poset*, which means *Pre Order Set*.




