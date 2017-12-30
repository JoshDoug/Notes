# Java Language

* [General Oracle Documentation](http://docs.oracle.com/en/)
* [Java 9 Early Access Documentation](https://docs.oracle.com/javase/9/)

## Variables

### Strings and characters

A character literal is always wrapped in single quotes: `char c1 = '1';` whereas a string literal is always wrapped in double quotes. A character is a primitive data type and contains a single character, whereas a String is a complex object which can consist of multiple characters.

A character can also be declared using a literla that's a Unicode escape sequence: `char dollar = '\u0024';`, this would contain a dollar sign character.

Because a `char` is a primitive it has no methods of its own, but the static `Character` class can be used instead.

When comparing strings use the `String` classes equals methods.

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

## Objects

An object is an instance of a class. A nonprimitive variable references an object, objects can have multiple references.

## Conditional Logic

If-Else shorthand: `String s = condition ? trueValue : falseValue;`, condition can be an expression in parentheses as well as a primitive boolean.

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

Usage:

LocalDate
LocalTime
LocalDateTime

For logging: `Instant.now()`

Durations, an example:

```Java
duration = Duration.ofHours(6);
duration = duration.multipliedBy(3);
duration = duration.plusMinutes(30);

dt = LocalDateTime.now();
dt = dt.plus(duration);
```