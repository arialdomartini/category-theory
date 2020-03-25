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
The simplest orders is the pre-orders: it's a relation that satisfies the minimun of conditions, composibility:

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

A category with these characteristics is called a *thin category* or *posetal category*. *Posetal* comes from *poset*, which means *Pre Order Set*.


## This categories and Homsets
The set of morphisms is called *homset*.

The set of morphisms from object `a` to object `b` in a category `C` is written as `C(a, b)`. There is also `C(a,a)`. It's a set. A thin 

A *thin category* is a category whose homsets each contain at most 1 morphism, that is is a category in which every homset is either an empty set or a singleton set.


## Partial order
We can impose additional conditions to a pre-order and get to a partial order. The next condition is to avoid loops. A partial order is a directed acyclic graph (DAG).

In a partial order some objects are not comparable at all, because there mustn't be an arrow between any 2 objects in the category.

## Total order
An order in which there is an arrow between any 2 pair of objects.


## Invertible
We once said that in a category, something that is both an epimorphism and a monomorphism needn't necessarily be reversible. Partial orders are the first example. In set theory, those corrspond to injective and surjective, and when a function is both, it is bijective, and hence invertible.

The definitions were:

```haskell
f : a -> b is an epimorphism if for any g, g' : b -> c

g . f = g' . f => g = g'

f is a monomorphis if for any h, h': c -> a

f . h = f . h' => h = h'
```

In a thin category this is satisfied by definition, because between `a` and `b` there could be at most 1 morphism, so `g` and `g'` are the same by definition. So, every arror in a thin category is an epimorphism and a monomorphism, at a same time.


## Monoid
In a one-element category we are not constraint to have one single arrow. We can have many more morphisms, and for each we can have compositions.

```haskell
M

id : m -> m 
f : m -> m
g : m -> m
g . f : m -> m
f . g : m -> m
```

etc.

A one-element category is called *monoid*.

In Set Theory a monoid is a set with some binary operator defined in it, with 2 conditions:

* it defines a *unit*, so that an element multiplied by the unit returns the element itself: `for each a there esist e such as e * a = a * e = a`
* associativity: `(a * b) * c = a * (b * c)

The binary operator must be defined for any pair of elements, it must be a total function.

Natural numbers with multiplication is a Monoid (having unit `1`). Also, natural numbers with sum is a Monoid. Unit is `0`. In this last example, each arrow would correspond to operations such as *adding 1* or *adding 2*.

The binary operation needn't be simmetric. For example, Strings and concatenation is a Monoid, with empty string as unit.


`M` only has one single object `m`. Its homset is `M(m,m)`. For any 2 elements in the homset, there is a 3rd element representing the product, the composition of them. This homset is the monoid as defined above, for the Set Theory. The identity in Category Theory corresponds to the unit in Set Theory.

## In programming
A Category of Types coresponds to a system that is strongly typed: you can compose only functions whose types match. Not any 2 functions are composable. A monoid is a special category: that corresponds to languages that are weak typing.
