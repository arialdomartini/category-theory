The Essence of Composition
================================

## What's a Category

 * Objects
 * Arrows (Morphisms)

 Categories are an abstraction, which means you take something and remove (subtract) details from it until you get the essence.

* **Do**: add examples of Categories

* Compositions of Morphisms: it is not optional.

### Example

Example of coposition of morphisms with composition of functions  
    * **Do**: examples in C# and Scala

### Properties of composition

#### Associativity
 
 ```haskell
 h ∘ (g ∘ f) = (h  ∘ g)  ∘ f = h  ∘ g  ∘ f
 ```
 
 #### Existence of Unity of Composition.
 
 For each object A, for each morphism starting from or ending to f, there exist a morphisms 
  
  ```haskell
  idA | f ∘ idA = f
  ```
  
  * **Do**: examples; also include examples of violations
  
  In Haskell:
  ```haskell
  id:: a -> a
  id x = x
   ```
  
  ### Notes
  Composition is the essence of programming
        
    
    
    

