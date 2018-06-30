The Essence of Composition
================================

* What's a Category
    * Objects
    * Arrows (Morphisms)
    * **Do**: add examples of Categories
    * Compositions of Morphisms: it is not optional.
        * Example of coposition of morphisms with composition of functions  
        * **Do**: examples in C# and Scala
        * Properties of composition
            * Associativity
            ```haskell
              h ∘ (g ∘ f) = (h  ∘ g)  ∘ f = h  ∘ g  ∘ f
            ```
            * Existence of Unity of Composition: for each object A, for each morphism starting from or ending to f, there exist a morphisms 
            ```haskell
              idA | f ∘ idA = f
            ```
            * **Do**: examples; also include examples of violations
              In Haskell:
              ```haskell
                id:: a -> a
                id x = x
              ```
        * Composition is the essence of programming
        
    
    
    

