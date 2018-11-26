The Essence of Composition
================================

## What's a Category

Just a collection of

 * Objects
 * Arrows (Morphisms)

and rules of *composition*.

### Composition

If there's a morphisms between `A` and `B` and a morphism that gows from `B` and `C`, then there *must* be a morphisms that goes from `A` to `C`, that is a composition of the 2 previous morphisms (details later on).

#### Functions as Morphisms

If `f :: A -> B` and `g :: B ->` then the composition `g` *after* `f` is

```
g ∘ f 
```

In C#:

```csharp
B f(A a) => 
  ... 
C g(B b) => 
  ...

C g_after_f(A a) => 
    g(f(a));
```
Note the right-to-left order of composition.


##### Composition in Haskell

```haskell
f :: A -> B
g :: B -> C

g_after_f :: A -> C
g_after_f = g . f 
```

##### Notes
* Categories are an abstraction, which means you take something and remove (subtract) details from it until you get the essence.
* Compositions of Morphisms: it is not optional.

### Properties of composition

#### Associativity
Composition is associative means there's no need for parenthesis:

In pseudo-haskell (it's pseudo since equality between functions is not defined):

```haskell
f :: a -> b
g :: b -> c
h :: a -> c
 
h ∘ (g ∘ f) = (h  ∘ g)  ∘ f == h  ∘ g  ∘ f
```
 
#### Existence of Unity of Composition.
 
For each morphism `f :: a -> b` starting from `A` there exists a morphisms so that:
 
```haskell
 
f ∘ idA = f
```
valid for each object `a` in `A`.
  
Equally, for each morphism `f :: X -> A` ending to `A`, there exists a morphisms `idA` so that:
  
```haskell
f ∘ idA == f
```

When dealing with functions, the Identity Morphisms is implemented as the indentity function, that is a function that returns its input parameter:

```haskell
id :: a -> a
id x = x
```

This function is universally polymorphic.

* **Do**: examples; also include examples of violations

### Summarizing
A Category consists of objects and morphisms. Morphisms can be composed, and the composition is associative. For every object there exist an *Identity Morphism* that serves as a unit in composition.
  
## Composition is the essence of programming

Analogy between complexity of code and volume and surface:

* Surface is the information we need to handle when we compose chunks
* VOlume is the information we need in order to implement.

The idea of composition is that the surface area grows slower than the volume. Once a chunk is implemented we can forget about the implementation and only focus on how it interacts with the rest of the world, with other chunks.

In OOP, an idealized object is only visible through its abstract interface (it's all surface, with no volume). 

### Category Theory
Category Theory, in that sense, is very extreme, because it actively discourages us from looking inside ojbects, and only focus on how they interact with other objects. 
