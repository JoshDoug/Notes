# [Basic I/O](https://docs.oracle.com/javase/tutorial/essential/io/index.html)
Covers I/O, focusing on streams, also covers serialisation, and file io.

## [I/O Streams](https://docs.oracle.com/javase/tutorial/essential/io/streams.html)
An IO Stream represents nad input source or output destination. A stream can represent many kinds of sources and destinations, such as disk files, devices, other programs, memory arrays, network sockets, as well as supporting many different kinds of data, including simple bytes, primitive data types, localised characters, and objects. Streams can be used to just transfer data, or to manipulate and transform the data as well. At its heart a stream is a sequence of data.

A program uses an input stream to read data from a source and an output stream to write data to a destination.

### [Byte Streams](https://docs.oracle.com/javase/tutorial/essential/io/bytestreams.html)
Byte Streams handle IO of raw binary data.

Programs use byte streams to perform io of 8-bit bytes, all byte stream classes are descended from [InputStream](https://docs.oracle.com/javase/8/docs/api/java/io/InputStream.html) and [OutputStream](https://docs.oracle.com/javase/8/docs/api/java/io/OutputStream.html). There are several byte stream classes, but the example here uses file IO byte streams, FileInputStream and FileOutputStream, other byte streams are used in much the same way.

TODO: Link to github project example and remove code?

```
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;

public class CopyBytes {
    public static void main(String[] args) throws IOException {

        FileInputStream in = null;
        FileOutputStream out = null;

        try {
            in = new FileInputStream("baconIpsum.txt");
            out = new FileOutputStream("outagain.txt");
            int c;

            while ((c = in.read()) != -1) {
                out.write(c);
            }
        } finally {
            if (in != null) {
                in.close();
            }
            if (out != null) {
                out.close();
            }
        }
    }
}
```

Here the program is mostly centered around the simple loop which reads a byte from the input stream and writes it to the output stream, one at a time.

#### Always Close Streams
Closing a stream when it's no longer needed is very important (eek!), in the example a finally block is used to gurantee that the stream is closed even if an error occurs, this helps avoid serious resource leaks.

#### When to use byte streams
Byte streams should only really be used for the most primitive IO. Here, since the example file uses character data a better approach would be to use character streams. There are other streams for more complex data types.

### [Character Streams](https://docs.oracle.com/javase/tutorial/essential/io/charstreams.html)
Character Streams handle IO of character data, automatically handling translation to and from the local character set.

### [Buffered Streams](https://docs.oracle.com/javase/tutorial/essential/io/buffers.html)
Buffered Streams optimise input and output by reducing the number of calls to the native API.

### [Scanning and Formatting](https://docs.oracle.com/javase/tutorial/essential/io/scanfor.html)
Scanning and Formatting allows a program to read and write formatted text.

### [I/O from the Command Line](https://docs.oracle.com/javase/tutorial/essential/io/cl.html)
IO from the Command Line describes the Standard Streams and the Console object.

### [Data Streams](https://docs.oracle.com/javase/tutorial/essential/io/datastreams.html)
Data Streams handle binary IO of primitive data type and String values.

### [Object Streams](https://docs.oracle.com/javase/tutorial/essential/io/objectstreams.html)
Object Streams handle binary IO of objects.

## [File I/O](https://docs.oracle.com/javase/tutorial/essential/io/fileio.html)
Covers File IO, in particular NIO - new input output.

### [What is a Path?](https://docs.oracle.com/javase/tutorial/essential/io/path.html)
Examining the concept of a path on a file system.

### [The Path Class](https://docs.oracle.com/javase/tutorial/essential/io/pathClass.html)
The Path Class is the cornerstone class of the `java.nio.file` package.

### [Path Operations](https://docs.oracle.com/javase/tutorial/essential/io/pathOps.html)
Looks at methods in the `Path` class that deal with syntactic operations.

### [File Operations](https://docs.oracle.com/javase/tutorial/essential/io/fileOps.html)
Introduces concepts common to many of the file IO methods.

### [Checking a File or Directory](https://docs.oracle.com/javase/tutorial/essential/io/check.html)
Shows how to check a file's existence and its level of accessibility.

### [Deleting a File or Directory](https://docs.oracle.com/javase/tutorial/essential/io/delete.html)

### [Copying a File or Directory](https://docs.oracle.com/javase/tutorial/essential/io/copy.html)

### [Moving a File or Directory](https://docs.oracle.com/javase/tutorial/essential/io/move.html)

### [Managing Metadata](https://docs.oracle.com/javase/tutorial/essential/io/fileAttr.html)
Explains how to read and set file attributes.

### [Reading, Writing, and Creating Files](https://docs.oracle.com/javase/tutorial/essential/io/file.html)
Shows the stream and channels methods for reading and writing files.

### [Random Access Files](https://docs.oracle.com/javase/tutorial/essential/io/rafs.html)
Shows how to read or write files in a non-sequential manner.

### [Creating and Reading Directories](https://docs.oracle.com/javase/tutorial/essential/io/dirs.html)
Covers APIs specific to directories, such as how to list a directory's contents.

### [Links, Symobolic or Otherwise](https://docs.oracle.com/javase/tutorial/essential/io/links.html)
Covers issues specific to symbolic and hard linkes.

### [Walking the File Tree](https://docs.oracle.com/javase/tutorial/essential/io/walk.html)
Demonstrates how to recursively visit each file and directory in a file tree.

### [Finding Files](https://docs.oracle.com/javase/tutorial/essential/io/find.html)
Shows how to search for files using pattern matching.

### [Watching a Directory for Changes](https://docs.oracle.com/javase/tutorial/essential/io/notification.html)
Shows how to use the watch service to detect files that are added, removed, or updated in one or more directories.

### [Other Useful Methods](https://docs.oracle.com/javase/tutorial/essential/io/misc.html)
Covers important APIs that didn't fit in prior sections.

### [Legacy File IO Code](https://docs.oracle.com/javase/tutorial/essential/io/legacy.html)
Shows how to leverage Path functionality with older code using the `java.io.File` class, with a table mapping the `java.io.File` API to `java.nio.file`.