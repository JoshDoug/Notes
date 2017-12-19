# C

* [Code::Blocks IDE - old](http://www.codeblocks.org/)
* [CLion - requires subscription](https://www.jetbrains.com/clion/)
* [Xcode](https://developer.apple.com/xcode/ide/)
* [ISO JTC SG WG for C](http://www.open-std.org/jtc1/sc22/wg14/) (Joint Technicall Committee, Sub-Committee, Working Group)
* The C Programming Language
* [Coding Guidelines](http://www.coding-guidelines.com/) - has some interesting links
* [COX Coding Guidelines](http://c0x.coding-guidelines.com/) - outdated?
* [C: A Reference Manual, 5th Ed.](http://careferencemanual.com/)
* [GNU C Library](https://www.gnu.org/software/libc/documentation.html)
* [DevDocs C Documentation](https://devdocs.io/c/) - similar to Java's online docs
* [CPP C Reference](http://en.cppreference.com/w/c)

## Preprocssor Commands

Directives:

* `#include <file>` - used for system header files located in the standard list of system directories
* `#include file` - user for header files in your own programs (or just any non-standard header file?)
* `#define name` - used to define a macro, e.g. `#define BUFFER_SIZE 1024`, then just refer to `BUFFER_SIZE` in the code, is this a constant then?

## Types

* ints, floats, doubles, long doubles, signed and unsigned, etc
* float - floating point number
* double - like float, but with twice the memory for larger floating point numbers. In print statements its designation is `lf` for 'long float'.
* booleans - Boolean types are not defined in the original C standard, so 0 is false, 1 is true. As of C99 boolean types have been added.

Use the `sizeof()` function to check the size of a type, e.g. `sizeof(char)`, `sizeof(unsigned short)`, or even `sizeof(void)`:

```C
printf("Storage size for an unsigned int: %lu bytes \n", sizeof(unsigned int));
```

## Basic IO

* `puts` - writes every char from the null-terminated string `\0` and on additional newline character `\n` to stdout.
* `printf`