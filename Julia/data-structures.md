# Julia Data Structures

Julia has three main types of data structures:

* Tuples
* Dictionaries
* Arrays

Note: Julai is 1 indexed!

## Tuples

Tuples are an immutable, ordered collection of elements.

```Julia
favourite_animals = ("penguins", "cats", "sugargliders") # Create tuple
favourite_animals[1] # Get value at position 1 (penguins)
favourite_animals[1] = "otters" # Tuples are immutable so we can't update it and this will cause a `MethodError`
```

## Dict

Dictonaries are mutable and can be used to store key-value pairs.

```Julia
phonebook = Dict("Jenny" => "867-5309", "Ghostbusters" => "555-2368") # Dict{String,String} with 2 entries
phonebook["Jenny"] # Grab Jenny's number
phonebook["Kramer"] = "555-FILK" # Add Kramer to the phonebook

# Delete Kramer from the phonebook
pop!(phonebook, "Kramer")
```

Dictariones aren't ordered so indexes cannot be used to retrieve items, instead an index will be interpreted as a key.

## Arrays

Arrays are essentially mutable tuples, they are mutable ordered collections. They can contain multiple types.

```
names = ["Ted", "Robyn", "Barney", "Lily", "Marshall"]
fibonacci = [1, 1, 2, 3, 5, 8, 13]
mixture = [1, 1, 2, 3, "Ted", "Robyn"]

names[3] # Returns "Barney"
names[3] = "Baby Bop" # Set index 3 to "Baby Bop" (strange name)
```

Arrays can also be edited using `push!` and `pop!` functions.

* Push adds an element to the end of an array
* Pop removes the last element of an array

```Julia
push!(fibonacci, 21) # Add 21 to the end of the array
pop!(fibonacci) # Remove the last value of the array (21)
```