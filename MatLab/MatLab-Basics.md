# MatLab - Matrix Labratory

Everything is a matrix, when `a = 1`, a is a 1x1 matrix.

* [MathWorks Tutorials](https://uk.mathworks.com/support)
* [MatLab Academy](https://matlabacademy.mathworks.com/)

## Variables

MatLab is a weakly typed language, variable types do not need to be declared.
By default, MatLab considers any variable to be a double, so 1 would be a double by default.

* Assignment: `a = pi` creates variable `a` and sets it to `pi`.
* Assignment with suppressed output: `b = pi;` assigns `pi` to `b` but doesn't display the result.
* String assignment: `c = 'Hello World'`, single or double quotes work.
* Optionally specify the type of a variable on assignment: `d = uint16(1)` would set to 1 with a class/type of an unsigned 16 bit integer, instead of a double.
* A vector or array: `e = [1 2 3]` or `e = [1,2,3]`, either works. This is still technically a matrix.

### Matrices

* `a = [1,2;3,4]` or `a = [1 2;3 4]`, commas don't seem to matter. This would set up a 2x2 matrix.

Output:

```matrix
1 2
3 4
```