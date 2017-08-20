# Generic Classes

Generics were introduced with Java 5 to help avoid runtime errors such as casting an object when retrieving it from a collection. Generics allo errors like this to be identified at compile time (and beforehand with a good IDE?).

Before generics were introduced, the object type was used to create container classes that could store any type of objects. This works fine but does allow for errors, specifically in casting. If you use an object and want to use it as an integer, you have to cast it as an integer.

The term *generic* can seem a bit misleading. When using a generic class, interface, or method, a concrete type must be specified, not very generic right? Well the class or interface is defined as generic behind the scenes so that it can be used for multiple data types without worrying about whether it's type safe or not. Generics are used by specifying parameterised types, these types are replaced by the compiler with conrete types at runtime, but the compiler checks them during compilation.

Classes, interfaces, methods, and even variables can be declared as generic types. Generic types must be reference types, they cannot be primitive data types. A generic type is a generic class or interface that is parameterised over types, if it is a subtype then it becomes a bounded type.

The benefits of generics are stronger type checks at compile time, this is of course easier to fix than runtime errors. It also eleminates unnecessary casts, and allows development of generic algorithms which can work on collections of different type.

## Comparable Interface Example

Without generics:

```java
// Prior to Java 1.5
public interface Comparable {
    public int compareTo(Object o);
}
```

With generics:

```java
// Comparable using generics
public interface Comparable<T> {
    public int compareTo(T o); //Where T stands for Type, similar to a placeholder, and is what makes the interface generic
}
```

That generic Comparable interface can then be used with any type.

Another Generic Example:

```java
//Prior to Java 5.0 - runtime error
Comparable c1 = new Date();
System.out.println(c1.compareTo("Monday")); //Date cannot be compared to a string, causes runtime error

//Using generics - compile time error, and will also be caught by the IDE
Comparable<Date> c2 = new Date();
System.out.println(c2.compareTo("Monday")); //No clumsy casting so caught by IDE or at compile time
```

## Syntax

Type parameters are delimited by angle brackets, the type follows the class name immediately. The class can have multiple type parameters.

Syntax for a generic class: `class name<T1, T2, ..., TN> {...}`

Type parameter names:

* E - Element (used extensively by Java Collections)
* K - Key
* N - Number
* T - Type, T is a generic Type
* V - Value (as in a primitive value?)

Syntax for a generic method: `public static <E> void print(E[] list) {...}`

For a method, the generic type is specified before the return type (which in the above example is void). The method expects an ArrayList of elements of type E.

Syntax for a generic interface: `public interface GenericInterface<K,V> {...}`

A generic interface can also have multiple type parameters, such as a pair of key value objects shown in the example above.

ArrayList example: