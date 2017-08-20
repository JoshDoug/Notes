# Java: Data Structures

A data structures stores objects and data primitives. Beyond storage, data structures provide operations for accessing and manipulating the data, and can be thought of as a container object that stores other objects or data primitives.

Collections are part of the [java.util package](https://docs.oracle.com/javase/8/docs/api/index.html).
Java 9 documentation (link might break), where collections are still part of the java.util package, which is part of the java.base module, [Java 9 documentation here](http://download.java.net/java/jdk9/docs/api/java/util/package-summary.html).

Collections are sometimes referred to as containers. They are used to store, retrieve, manipulate, and aggregate. Java has two types of contianers. Some containers store a collection of elements, other containers store key-value pairs, called maps.

## Links

* [Java Collections Trail](http://docs.oracle.com/javase/tutorial/collections/index.html)
* [Collections Framework Documentation: Overview, API Outline, Design Rationale](http://download.java.net/java/jdk9/docs/api/java/util/doc-files/coll-index.html)
* [JavaDoc](http://download.java.net/java/jdk9/docs/api/java/util/package-summary.html)

## Types of Data Structures

* A data structure is a way of collecting and organising data.
* Choosing the right data structure impacts efficiency.
* Data comes from many sources, such as databases and files.
* Many data structures are implemented as linked lists.

Types:

* Lists - store an ordered collection of elements (ArrayList, LinkedList..)
* Set - stores a group of nonduplicate elements
* Queue - stores objects that are processed in FIFO order
* ArrayList - stores objects and can grow and shrink.
* LinkedList - uses pointers to keep track of elements
* Vector - can grow and shrink; provides synchronisation
* Stack - operates on last in, first out (LIFO)
* Queue - operates on first in, first out (FIFO)

ArrayList and Vector Advantages:

* Provide fast access using indexing
* Memory coherence
* Provide an intial size (optional)
* Use interal arrays for storage, which makes random access fast.

Disadvantages:

* Adding elements to the middle can be time consuming (gotta shift everything over)
* Waste space if array is not full
* Need to be resized when they reach capacity (although this is done automatically, it is still time consuming)
* Slower when deleting elements from the middle

LinkedList Advantages:

* Insertion and deletion operations are easily implemented
* Elements are effeciently added or deleted from the middle of the list (just change the sibling links instead of shifting everything over)

So probably fine if you want to access data sequentially.

Disadvantage:

* Elements in a linked list must be read sequentially, since each element points to the next element.
* Elements are not stored sequentially in memory (as they are in an ArrayList)
* Random access to elements can be inefficient (gotta read each preceding element to get to the one you want)
* Slower iterations and extra memory overhead required (in order to keep track of the pointer to the next element in the list)

## Using Data Structures

### Collection Interface

Diagram that shows (some of) the data structures that implement the Collection interface and their hierarchy:

![Collection Interfaces](../../Assets/CollectionsDiagram.png)

The Collection interface defines common operations for data structures. it provides basic operations for add and remove (or enforces it, right?), it also provides important query operations such as getting the length of a collection.

Other enforced methods are toArray(), or to convert from an array to a list, use Arrays.toList().

There is also a Collections class that provides static methods to sort, search, copy, and fill data structures as long as they implement interfaces relevant to the operation.

### Iterable Interface

Each collection has an Iterator object to traverse the elements. This provides tools for walking through a data structure and hides the details of how data is stored. The Collection interface extends the Iterable interface.

The Iterable interface enforces 3 methods, iterator(), forEach(), and spliterator()...?

The iterator() method returns an Iterator object. This can then be used to walk the collection using hasNext() and next() and to remove elemnents from it in a safe way.

In addition to the Iterable interface, there is a ListIterator, which is used for list data structures, e.g. LinkedLists. This adds functionality such as traversing a list backwards using previous(), hasPrevious(), and previousIndex() methods.

### ArrayLists

The ArrayList is probably the most frequently used data structure (certainly in my case), and like the LinkedList it implememnts the List interface. The ArrayList approach to implementing the List interface is to define an object array and increase the size of that array as necessary to support the number of elements contained within the collection.

* ArrayLists can contain duplicate elements and null values.
* An ArrayList isn't inherently thread safe, so modifications need to be synchronised.
* Quick access is provided to elements based on index position, elements can be added or removed by index value.

### LinkedLists

### Vectors

### Stacks

### Queues