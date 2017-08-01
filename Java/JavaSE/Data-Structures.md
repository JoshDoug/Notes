# Java: Data Structures

A data structures stores objects and data primitives. Beyond storage, data structures provide operations for accessing and manipulating the data, and can be thought of as a container object that stores other objects or data primitives.

Collections are part of the [java.util package](https://docs.oracle.com/javase/8/docs/api/index.html).
Java 9 documentation (link might break), where collections are still part of the java.util package, which is part of the java.base module, [Java 9 documentation here](http://download.java.net/java/jdk9/docs/api/java/util/package-summary.html.

## Types of Data Structures

* A data structure is a way of collecting and organising data.
* Choosing the right data structure impacts efficiency.
* Data comes from many sources, such as databases and files.
* Many data structures are implemented as linked lists.

Types:

* ArrayList - stores objects and can grow and shrink.
* LinkedList - uses pointers to keep track of elements
* Vector - can grow and shrink; provides synchronisation
* Stack - operates on last in, first out (LIFO)
* Queue - operates on first in, first out (FIFO)

![Collection Interfaces](../../Assets/CollectionsDiagram.png)

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