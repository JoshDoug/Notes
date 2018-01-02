# Java Language

* [General Oracle Documentation](http://docs.oracle.com/en/)
* [Java 9 Early Access Documentation](https://docs.oracle.com/javase/9/)

## Variables

### Strings and characters

A character literal is always wrapped in single quotes: `char c1 = '1';` whereas a string literal is always wrapped in double quotes. A character is a primitive data type and contains a single character, whereas a String is a complex object which can consist of multiple characters.

A character can also be declared using a literla that's a Unicode escape sequence: `char dollar = '\u0024';`, this would contain a dollar sign character.

Because a `char` is a primitive it has no methods of its own, but the static `Character` class can be used instead.

When comparing strings use the `String` classes equals methods.

#### String Building

To avoid allocating multiple objects when manipulating many Strings, the `StringBuilder` class can be used.

```Java
StringBuilder sb = new StringBuilder("Hello")
    .append(", ")
    .append("World")
    .append("!");
System.out.println(sb); // Implicitly calls .toString() on sb
```

This could be done in one line, but it's just to demonstrate the use. It would most likely make sense to use when constructing a string from variables whose values are not known ahead of time (e.g. when looping through an array) or with user input.

### Numbers

Postfix and Prefix Incrementing:

With `int value1 = 10;` & `int value2 = 10`:

* Postfix: `System.out.println(value1++);` - output would be 10, but `value` would now be 11.
* Prefix: `System.out.println(++value2);` - ouput and value would be 11.

Using underscore, '_', seperators in lengthy numbers:

* `long bigNum = 10_000_000`
* `long bigNum = 10000000`
* Both have the same value in Java, but the first uses underscores so it is easier to read.
* Introduced in Java 7
* Another example: `double value = 1_234_567.89`

Formatting primitives when converting them to strings:

```Java
long bigNum = 10_000_000;
NumberFormat formatter = NumberFormat.getNumberInstance();
String formattedBigNum = formatter.format(bigNum);
System.out.println(formattedBigNum);
```

* The output here would be the String: `10,000,000`, nicely formatted.
* The formatter can be configured by using a `Locale` instance in the constructor method (`NumberFormat.getNumberInstance(locale)`)
* Same can be done for currency: `NumberFormat.getCurrencyInstance(new Locale("da", "DK"));`, this would format the currency for Denmark.

Using `BigDecimal`, because `double` isn't always exact:

```Java
jshell> double value = .012
value ==> 0.012

jshell> double pSum = value + value + value;
pSum ==> 0.036000000000000004 // !!
```

```Java
BigDecimal value = new BigDecimal(.012);
BigDecimal bSum = value.add(value).add(value);
```

Here `bSum` will equal 0.036. [BigDecimal JavaDoc](https://docs.oracle.com/javase/9/docs/api/java/math/BigDecimal.html).

Dividing ints with a decimal result:

```Java
int num1 = 56;
int num2 = 42;
double result = (double) num1 / num2;
```

At least one of the numbers in a division has to be a double otherwise the result is truncated or rounded (which is it?). In the above example one of the numbers is cast to `double` to deal with this.

Rounding a number:

```Java
double value = -3.99999
long roundedValue = Math.round(value); // round returns a long
```

Boolean initalisation can be done from the evaluation of an expression:

```Java
int num = 0;
boolean example = (num != 0);
```

Here example would be false. This is neater than using a redundant if-else statement to evaluate the expression and then set the boolean value.

## Arrays

Simple arrays:

* `int[] ints = {1, 2};`
* `int ints[] = {1, 2};` - valid but weird
* Not resizable, size can either be set manually, or implicitly (see above, each array will have a lenght of 2)
* `String[] strings = {"This", "is", "a", "String", "array"};` - can create arrays of objects as well
* `int[] sized = new int[10];` - create an empty array with a size of 10
* `Object objects[] = new Object[10];` - Example array of Objects (other than String)

Manipulating arrays:

* `Arrays.sort(ints);` - use the Arrays class static methods to manipulate arrays
* `System.arraycopy(sized, 5, copied, 0, 5)` - copy array sized from index 5 into copied from 0 to 5

Two-dimensional arrays (always forget these exist):

```Java
String[][] states = new String[3][2]; // Kind of like a matrix?
states[0][0] = "California";
states[0][1] = "Sacramento";

states[1][0] = "Oregon";
states[1][1] = "Salem";

states[2][0] = "Washington";
states[2][1] = "Olympia";
```

* When using `states.length` this will refer to the outermost array/leftmost array, in this case the number is 3.
* Arrays can have more than 2 dimensions, but this would be quite an unusual use case.

## Objects

An object is an instance of a class. A nonprimitive variable references an object, objects can have multiple references.

## Constants

While Java does have a `const` keyword, it's not implemented. Instead the `final` keyword is used.

Constants can be usefully used on a class instead of using enums like so: `public static final String EXAMPLE = "ExampleValue";`, these don't need to be encapsulated and can be public because they're a constant.

* It's convention to make a static constant upper case.
* Constants can be local variables as well: `final String example = "exampleValue";`

## Enums

Short for enumeration, enums can be nested within a class (like an anonymous class) or as a separate class.

## Conditional Logic

If-Else shorthand: `String s = condition ? trueValue : falseValue;`, condition can be an expression in parentheses as well as a primitive boolean.

Switch statement, because I always forget the syntax:

```Java
switch (monthNumber) {
    case 1:
        System.out.println("The month is January");
        break;
    case 2:
        System.out.println("The month is February");
        break;
    case 3:
        System.out.println("The month is March");
        break;
    default:
        System.out.println("A month after March");
}
```

As of Java 7 switch statements work with Strings as well as int, byte, char, and short.

## Lambdas

Lambdas are just functions, useful to replace code like anonymous inner classes.

## Parallel Streams

Iterate over a collection with declarative code using a parallelised filter map reduce lambda.

Example, get the max weight of a man from a collection for people objects, in parallel:

```Java
int highestWeight = people.parallelStream()
                          .filter(p -> p.getGender() == MALE)
                          .mapToInt(p -> p.getWeight())
                          .max();
```

Neat.

## Default Methods

Add a default method to an interface:

```Java
interface Collection<T> {
    ...
    default Stream<T> stream() {
        ...
    }
}
```

Example of a default method used in the Collections API provided by Java itself, added in JDK8.

## Method References

A shorthand you can use in lambdas, that might not actually be much shorter:

```Java
list.replaceAll(s -> s.toUpperCase());
list.replaceAll(String::toUpperCase);

list.sort(Comparator.comparing(p -> p.getName()));
list.sort(Comparator.comparing(Person::getName));
```

But I guess it cuts down on the number of parantheses which is a plus.

## Date Time APIs - JSR 310

* New addition replaces java.util.Date, Calendar, TimeZone, DateFormat
* Fluent, Immutable, Thread Safe, Easy to use
* Interoperable with java.util.Date/Calendar
* ISO 8601
* Introduced with Java 8

Usage:

* `LocalDate`
* `LocalDateTime`
* `LocalTime`
* `DateTimeFormatter`

For logging: `Instant.now()`

Durations, an example:

```Java
duration = Duration.ofHours(6);
duration = duration.multipliedBy(3);
duration = duration.plusMinutes(30);

dt = LocalDateTime.now();
dt = dt.plus(duration);
```