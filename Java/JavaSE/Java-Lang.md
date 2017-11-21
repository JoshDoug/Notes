# Java Language

* [General Oracle Documentation](http://docs.oracle.com/en/)
* [Java 9 Early Access Documentation](https://docs.oracle.com/javase/9/)

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