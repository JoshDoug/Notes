# MatLab - Matrix Labratory

Everything is a matrix, when `a = 1`, a is a 1x1 matrix.

* [MathWorks Tutorials](https://uk.mathworks.com/support)
* [MatLab Academy](https://matlabacademy.mathworks.com/)

## Variables

MatLab is a weakly typed language, variable types do not need to be declared.
By default, MatLab considers any variable to be a double, so 1 would be a double by default.
Datastructures in MatLab are typically Scalar (single value), Vector (an array of values), or Matrix (grid of values), but really everything is a matrice, a scalar value is just a 1x1 matrix, a vector is just a 1xN matrix.

* Assignment: `a = pi` creates variable `a` and sets it to `pi`.
* Assignment with suppressed output: `b = pi;` assigns `pi` to `b` but doesn't display the result.
* String assignment: `c = 'Hello World'`, single or double quotes work.
* Optionally specify the type of a variable on assignment: `d = uint16(1)` would set to 1 with a class/type of an unsigned 16 bit integer, instead of a double.
* A scalar: `x = 1`, with a class of double, and which is really a 1x1 matrix.
* A vector or array: `e = [1 2 3]` or `e = [1,2,3]`, either works. This is still technically a matrix.

### Matrices

* `a = [1,2;3,4]` or `a = [1 2;3 4]`, commas don't seem to matter. This would set up a 2x2 matrix.

Output:

```matrix
1 2
3 4
```

Matrix of matrices: create four matrices, e.g. `a = [1,2;3,4]` x4, these can then be made into a 'super matrix' using a slightly different syntax: `e = {a,b;c,d}`, which is also accessed with that syntax, so to get `a` use `e{1,1}`

#### 3D Matrix

* Defining an all zero 3D matrix `zero(2,2,2)`, this creates a 2x2x2 matrix of zeros. MatLab display it in slices.
* `ones()` creates a matrix filled with ones, `rand()` creates a matrix with number between 0 and 1, `randn()` creates a matrix of normally distributed random numbers.

Parts of the matrix can be specified and set to other values easily, so a 2x2x2 matrix `a`, set to all zeroes like so `a = zeroes(2,2,2)` can be changed to have the 2nd slice (or 2nd z index) to a different matrix like so: `a(:,:,2) = [1,2;3,4]`. MatLab arrays start at 1, not 0.

### Structures

Structures are a storage mechanism allowing multiple peices of data to be associated, similar to an array of objects.
A structure is built up via a name.attribute, so for example a structure of people could be started with the name: `person.name = 'John Doe`, then the address could be set with `person.address = "Fake Address 1"`, this on its own is similar in concept to an object, but it can be extended to multiple of these objects very easily. To add a second person: `person(2).name = "Joe Bloggs` and `person(2).address = "Fake Address 2"`. As this is MatLab this structure is still considered a matrix.