Types and Functions
========================

## Types
* Relation between Types and Composition
* What are Types: sets of values
    * Bool, Integers as finite sets
    * String and Haskell Integers as infinite sets
* **Do**: Functions implemented with Dictionaries
* Sets is a kind of Category
* Haskell types are a Category
    * Each Haskell type also include bottom ⊥ to represent the possibility of non-terminating calculation
        * `undefined` to represent ⊥
* Pure and unpure functions

## Sets
### The empty set
* It's not Scala/C#'s `void`
* The `absurd` function:

```haskell
absurd :: Void -> a
```

#### The singleton set
* `Unit` in Haskell. represented by `()` a symbol used to represent 3 things: the Type, the Value and the Constructor
* It has one single value. This value just "is"

##### Morphisms from `()`
    * We can replace explicit mention of any value with funcions from `()`:
 ```haskell
 f44 :: () -> Int
 f44 () => 44
 ```
 
 So, we can replace the value 44 (contained in the Int set, or in the object Int of the Hask category) with `f44` which is a morhism
##### Morphisms to `()`
In imperative languages, are functions with side effect. In Haskell functions cannot have side effects, so funcions to `()` just ignore their argument:
```haskell
fInt :: Integer -> ()
fInt _ = ()
          
unit :: a -> ()
unit _ = ()
```
### Sets with 2 elements
* Bool
* Functins to Bool are called predicates
        
        
