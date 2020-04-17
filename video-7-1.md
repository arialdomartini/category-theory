Functoriality, bifunctors
=========================

## Functors and Endofunctors
So we saw that

* Functors are mapping *between* categories
* Endofunctors are mapping *within* a category

The rules are just the same.

A Functor is like a number of functions put together.

* There is one major function that map objects (and this is an actual function only if the category is small, that is, only if its objects form a set)
* But it also has to preserve the structure of category, hence Functor maps the connections between objects, the morphisms: for each pair of objects we have the set of morphisms, the hom-set, and we define a mapping between hom-sets to the corresponding hom-sets in the othere category, and the mapping is a function.

We also saw that Functors must preserve the categorical structure, that is identity and composition.

## Functor composition

Now, since Functors are built from functions, we know that functions compose. Maybe we can compose functors.

Say we have a functor `F` from category `C` to `D` and one `G` from `D` to `E`. We can think of a functor which is the composition of `F` and `G`.

Object `a` would be mapped through `F` as `F a` and through `G` in `E` as `G(F a)`. Also morphisms would be. For example, `f :: a -> b` would be mapped into `D` with `F` as `F f`, and into `E` with `G` as `G (F) f`. We are not doing nothing special: this is just function compositions. `F` is a function on objects, `fmap` is a function on hom-sets: after all, they are just functions.

### Identity Functor
Since we have composition of functors, it's legit to ask if there is identity. It must be a functor that maps object on themselves, and each morphisms to itself, without changing anything. This identity functor is of course an endofunctor. It must obey 

```haskell
id . F = F
F . id = F
```

### Cat
Whatever we learn on functions, we can apply to functors.

So, it's a category! It's a category in which objects are categories, and morphisms are functors. This category is called *Cat*.

There are some subtle details. We know that categories can be small or large (see [Chapter 3 - Categories Great and Small](chapter-3.md)), and things can become a bit complicated. In case we have a category of large categories, we have to use a more powerful tool: we will get to it later.

#### Example
Let's try to compose 2 functors in programming: `Maybe` and `List`. Let's consider the function `tail :: [a] -> [a]` which returns the tail of a list, throwing away the head of a list. This function is defined only for non-empty lists. If the list is not empty, the program dies. That's bad, especially because this function is in the core library.

To be safer, let's define:

``` haskell
safeTail :: [a] -> Maybe [a]
safeTail [] = Nothing
safeTail (x : xs) = Just xs
```

`Maybe List a` is also a Functor. Let's say we want to apply square to the value of items in `Maybe List Int`: we could of course define a function, like we have just done with `safeTail`, but it's a pity: we already have `fmap` for `Maybe` and `fmap` for `List`.

``` haskell
square :: Int -> Int
square x = x * x * x
```

We want to apply this function to some Maybe list `mis :: Maybe [Int]`. We need to apply something `??` to `mis`.

``` haskell
fmap ?? mis
```

Now, this function `??` must be an `fmap` itself, because it must operate on `[Int]`:

``` haskell
fmap (fmap square) mis
```

In other words, we need to jump 2 layers of functors. We can write it as:

``` haskell
(fmap . fmap) square mis
```





