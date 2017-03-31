# Java Annotations - those weird @ things the IDE tells you to add
Oracle's Java Tutorial for Annotations: https://docs.oracle.com/javase/tutorial/java/annotations/index.html

Annotations are a form of metadata about a program but are not part of the program itself and have no direct effect on the operation of the code they annotate.

They have a number of uses:
* Information for the compiler - to detect errors or supress warnings
* Compile-time and deployment-time processing - Software tools can process annotation information to generate code, XML files, etc
* Runtime processing - Some annotations are available to be examined at runtime

An annotation: `@Entity`, the @ signifies to the compiler that it is an annotation. An annotation can include elements, which can be named or unnamed, and have values:
```
@Author(
    name = "JoshDoug",
    date = "3/27/2014"
  )
  class DemoClass() {...}
```
or
```
@SuppressWarnings(value = "unchecked")
void aMethod() {...}
```
if there is only a single element called value, then the name can be omitted:
```
@SuppressWarnings("unchecked")
void aMethod() {...}
```
if there are no elements, the parentheses can be omitted as well:
```
@Override
void aMethod() {...}
```

Multiple annotations can be applied to the same declaration:
```
@Author(name = "Jane Doe")
@EBook
class ExClass {...}
```

The same type of annotation can be repeated, this is called a repeating annotation (supported as of JavaSE 8):
```
@Author(name = "Jane Doe")
@Author(name = "Joe Bloggs")
class ExClass {...}
```

## Where Annotations Can Be Used
Annotations can be applied to declarations: declarations of classes, fields, methods, and other program elements.
