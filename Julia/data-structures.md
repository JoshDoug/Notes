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

* `d = Dict()` creates an empty dictionary with any types: `Dict{Any,Any}`
* `d = Dict("Josh" => 8675309)` initialises a dictionary of type `Dict{String,Int64}` and the key-value pair `"Josh":8675309`
* `d = Dict{Any, Any}("Josh" => 8675309)` is the same as the above, but sets the types to `Any`
* Initialising with multiple entries of different types will also set the type to `Any`

Dictariones aren't ordered so indexes cannot be used to retrieve items, instead an index will be interpreted as a key.

## Arrays

Arrays are essentially mutable tuples, they are mutable ordered collections. They can contain multiple types.
Arrays are passed by reference, so with `newarray = oldarray`, altering the `newarray` will also change the `oldarray`.
To make a new copy of an array use the `copy` function: `newarray = copy(oldarray)`

```
names = ["Ted", "Robyn", "Barney", "Lily", "Marshall"]
fibonacci = [1, 1, 2, 3, 5, 8, 13]
mixture = [1, 1, 2, 3, "Ted", "Robyn"]

names[3] # Returns "Barney"
names[3] = "Baby Bop" # Set index 3 to "Baby Bop" (strange name)
```

Arrays can also be edited using `push!` and `pop!` functions.

* Push adds an element to the end of an array: `push!(an_array, "value")`
* Pop removes the last element of an array: `pop!(an_array)`

```Julia
push!(fibonacci, 21) # Add 21 to the end of the array
pop!(fibonacci) # Remove the last value of the array (21)
```

Arrays can have multiple dimensions, a 1D array in Julia can also be known as a vector.

Arrays can contain other arrays:

```Julia
favorites = [["koobideh", "chocolate", "eggs"],["penguins", "cats", "sugargliders"]]

#= Output:
2-element Array{Array{String,1},1}:
 String["koobideh", "chocolate", "eggs"]   
 String["penguins", "cats", "sugargliders"]
=#

numbers = [[1, 2, 3], [4, 5], [6, 7, 8, 9]]

#= Output:
3-element Array{Array{Int64,1},1}:
 [1, 2, 3]   
 [4, 5]      
 [6, 7, 8, 9]
=#
```

And arrays can be multidimensional:

```Julia
rand(4, 3)

#=
The 2 after Float64 denotes that this is a 2 dimensional array
4×3 Array{Float64,2}:
 0.300588    0.672733  0.899022
 0.0616459   0.144716  0.437821
 0.00268334  0.203593  0.324109
 0.0626902   0.391251  0.632736
=#

rand(4, 3, 2)

#=
This creates a 3 dimensional array of random numbers between 0 and 1.
The array has 4 rows, 3 columns, and 2 layers.

4×3×2 Array{Float64,3}:
[:, :, 1] =
 0.806548  0.0587993  0.414702
 0.668817  0.664251   0.483232
 0.933614  0.460968   0.38814 
 0.983742  0.698005   0.467232

[:, :, 2] =
 0.180356  0.0633663  0.960375 
 0.840386  0.195604   0.0780185
 0.797932  0.814768   0.677171 
 0.955011  0.763886   0.490048 
=#
```