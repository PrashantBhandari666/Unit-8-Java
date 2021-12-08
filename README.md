# I/O and Stream

## ``java.io`` package
-----------------------
``java.io`` package provides classes for system input and output through data streams, serialization and the file system.

## I/O Stream:
---------------

A stream is a method to sequentially access a file. I/O Stream means an input source or output destination representing different types of sources e.g. disk files.The java.io package provides classes that allow you to convert between Unicode character streams and byte streams of non-Unicode text.

* ``Stream`` – A sequence of data.
* ``Input Stream``: reads data from source.
* ``Output Stream``: writes data to destination.`

### **Byte Stream**

Java byte streams are used to perform input and output of 8-bit bytes. Though there are many classes related to byte streams but the most frequently used classes are, ``FileInputStream`` and ``FileOutputStream``.

**Example:**
```Java
import java.io.*;

public class CopyFile {

    public static void main(String args[]) throws IOException {
        FileInputStream in = null;
        FileOutputStream out = null;

        try {
            in = new FileInputStream("input.txt");
            out = new FileOutputStream("output.txt");
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

### **Character Stream:**

Java Byte streams are used to perform input and output of 8-bit bytes, whereas Java Character streams are used to perform input and output for 16-bit Unicode. Though there are many classes related to character streams but the most frequently used classes are, ``FileReader`` and ``FileWriter``. Though internally ``FileReader`` uses ``FileInputStream`` and ``FileWriter`` uses ``FileOutputStream`` but here the major difference is that ``FileReader`` reads two bytes at a time and ``FileWriter`` writes two bytes at a time

**Example:**
```Java
import java.io.*;

public class CopyFile {

    public static void main(String args[]) throws IOException {
        FileReader in = null;
        FileWriter out = null;

        try {
            in = new FileReader("input.txt");
            out = new FileWriter("output.txt");
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

**When to use Character Stream over Byte Stream?** 

* In Java, characters are stored using Unicode conventions. Character stream is useful when we want to process text files. These text files can be processed character by character. A character size is typically 16 bits.

**When to use Byte Stream over  Character Stream?** 

* Byte oriented reads byte by byte.A byte stream is suitable for processing raw data like binary files.

## Reading and Writing files
----------------------------
Java ``FileWriter`` and ``FileReader`` classes are used to write and read data from text files (they are Character Stream classes). It is recommended not to use the ``FileInputStream`` and ``FileOutputStream`` classes if you have to read and write any textual information as these are Byte stream classes.

### **``FileWriter``**
``FileWriter`` is useful to create a file writing characters into it.

* This class inherits from the OutputStream class.
* The constructors of this class assume that the default character encoding and the default byte-buffer size are acceptable. To specify these values yourself, construct an OutputStreamWriter on a FileOutputStream.
* FileWriter is meant for writing streams of characters. For writing streams of raw bytes, consider using a FileOutputStream.
* FileWriter creates the output file , if it is not present already.

**Constructor:**

* ``FileWriter (String fileName)`` – constructs a FileWriter object given a file name.
* ``FileWriter (String fileName, Boolean append)`` – Constructs a FileWriter object given a file name with a Boolean indicating whether or not to append the data written.

**Methods:**

* ``public void write (int c) throws IOException`` – Writes a single character.
* ``public void write (char [] stir) throws IOException`` – Writes an array of characters.
* ``public void write(String str) throws IOException`` – Writes a string.
* ``public void write(String str,int off,int len)throws IOException`` – Writes a portion of a string. Here off is offset from which to start writing characters and len is number of character to write.
* ``public void flush() throws IOException``: flushes the stream
* ``public void close() throws IOException``: flushes the stream first and then closes the writer.

**Example**:

```Java
import java.io.*;

public class FileWriterEx {

    public static void main(String args[]) throws IOException {
        String str="I am Prashant Bhandari";
        FileWriter fw = null;
        try {
            fw = new FileWriter("file.txt",true);
            fw.write(str);
        } finally {
            if (fw != null) {
                fw.close();
            }
        }
    }
}
```

### **``FileReader``**

``FileReader`` is useful to read data in the form of characters from a ‘text’ file.

* This class inherit from the ``InputStreamReader`` Class.
* The constructors of this class assume that the default character encoding and the default byte-buffer size are appropriate. To specify these values yourself, construct an ``InputStreamReader`` on a ``FileInputStream``.
* ``FileReader`` is meant for reading streams of characters. For reading streams of raw bytes, consider using a FileInputStream.

**Constructors:**

* ``FileReader(File file)``– Creates a FileReader , given the File to read from
* ``FileReader(FileDescripter fd)``– Creates a new FileReader , given the FileDescripter to read from
* ``FileReader(String fileName)`` – Creates a new FileReader , given the name of the file to read from

**Methods:**

* ``public int read () throws IOException`` – Reads a single character. This method will block until a character is available, an I/O error occurs, or the end of the stream is reached.
* ``public int read(char[] cbuff) throws IOException`` – Reads characters into an array. This method will block until some input is available, an I/O error occurs, or the end of the stream is reached.
* ``public abstract int read(char[] buff, int off, int len) throws IOException`` – Reads characters into a portion of an array. This method will block until some input is available, an I/O error occurs, or the end of the stream is reached.
   
    Parameters:

    * **buff** – Destination buffer

    * **off** – Offset at which to start storing characters

    * **len** – Maximum number of characters to read

* ``public void close() throws IOException`` closes the reader.
    
* ``public long skip(long n) throws IOException`` – Skips characters. This method will block until some characters are available, an I/O error occurs, or the end of the stream is reached.

    Parameters:

    * **n** – The number of characters to skip

**Example:**
```Java
import java.io.*;

public class FileReaderEx {

    public static void main(String[] args) throws IOException {
        {
            int ch;
            FileReader fr = null;
            try
            {
                fr = new FileReader("file.txt");
            }
            catch (FileNotFoundException fe)
            {
                System.out.println("File not found");
            }
            while ((ch=fr.read())!=-1)
                System.out.print((char)ch);
            fr.close();
        }
    }
}

```

## Serializable Interface
---------------------------
The ``Serializable`` interface is present in ``java.io`` package. It is a marker interface. A Marker Interface does not have any methods and fields. Thus classes implementing it do not have to implement any methods. Classes implement it if they want their instances to be Serialized or Deserialized. 

**Declaration**

```Java
public interface Serializable
```


## Serialization & Deserialization 
-----------------------------------

Serialization is a mechanism of converting the state of an object into a byte stream. Serialization is done using ``ObjectOutputStream``.

Deserialization is the reverse process where the byte stream is used to recreate the actual Java object in memory. This mechanism is used to persist the object. Deserialization is done using ``ObjectInputStream``.
