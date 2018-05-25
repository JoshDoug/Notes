# Julia Data Structures

Julia has three main types of data structures:

* Tuples
* Dictionaries
* Arrays

## Tuples

Tuples are an immutable, ordered collection of elements.

```Julia
favourite_animals = ("penguins", "cats", "sugargliders") # Create tuple
favourite_animals[1] # Get value at position 1 (penguins)
favourite_animals[1] = "otters" # Tuples are immutable so we can't update it and this will cause a `MethodError`
```