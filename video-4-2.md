Products
========

Again about Terminal Objects: we didn't say anything about outgoing arrows. There are usually outgoing arrows from Terminal Objects. These are the arrows that help us define the Generalized Elements: every arrow to an element can be used as the definition of the element.

Initial object and Opposite Category
====================================
We could just say, let's do the same already seen for Terminal Object, just reverse it. This trick is general. Every construction in category theory really has its opposite contruction, done by reversing arrows. This property is related to the fact that for every category we can always create another almost identical category in which all the arrows are reverted, the opposite category, so from `C` to `Copp`.

`C` might contain:

```haskell
f :: a -> b
g :: b -> c

g . f :: a -> c
```
plus the identities, while `Copp` whould contain:

```haskell
fopp :: b -> a
gopp :: c -> b

fopp . gopp = (g . f)opp :: c -> a
```

It's still a category.

Initial object is the Terminal object in the opposite category.
