# TypeScript

TypeScript is a typed superset of JavaScript that compiles to plain JavaScript. It's both an extension of the language and an ECMAScript transpiler.

* [TypeScript Site](https://www.typescriptlang.org)
* [Documentation](https://www.typescriptlang.org/docs/home.html)
* [Playground](https://www.typescriptlang.org/play/index.html)

## Types

* `var varName: type = value` e.g. `var greeting: string = "Hello World"`
* `function funcName(value: type)` e.g. `function speak(value: string)`
* `function funcName(value: type): type` e.g. `function speak(value: string): string`
* Types can be optionally added, so a method parameter doesn't need to have a specified type, nor does the method return type need to be made explicit.

## ES6 Features

Typescript supports several ES6+ features that it can then transpile to ES5 for older browser support.

* Default parameter syntax, this syntax is the same as the ES6 syntax
* Template strings, this syntax is the same as the ES6 syntax
* `let` - block scoped variables, sane var.
* `const` - variable constant that is also block scoped
* Supports `for..of` syntax
* Arrow functions (lambdas)
* Destructuring - assigning values in an array to a list of individual variables, or an object, and more.
* Spread operator - useful for function parameters, injecting an array into another array
* Computer properties - dynamic object property naming?

These are all well supported by modern browsers, but not IE, Opera Mini, etc.