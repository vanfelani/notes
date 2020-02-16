# File I/O

## Path
A file is identified by its path through the file system.  
Example:  
**Solaris OS:** `/home/sally/statusReport`  
**Windows:** `C:\home\sally\statusReport`  


### **Absolute and Relative Path**
A path is either relative or absolute. An absolute path always contains the root element and the complete directory list required to locate the file. A relative path needs to be combined with another path in order to access a file. 
Example:  
**Relative:** `/home/sally/statusReport`  
**Absolute:** `joe/foo`  


### **Symbolic Links**
A symbolic link is a special file that serves as a reference to another file. A symbolic link is also referred to as a symlink or a soft link. A symbolic link is usually transparent to the user. Reading or writing to a symbolic link is the same as reading or writing to any other file or directory.


## The Path Class
The `Path` class is a programmatic representation of a path in the file system. A `Path` object contains the file name and directory list used to construct the path, and is used to examine, locate, and manipulate files.


### **Creating a Path**
A `Path` instance contains the information used to specify the location of a file or directory. 
You can easily create a `Path` object by using one of the following get methods from the Paths (note the plural) helper class:

```java
Path p1 = Paths.get("/tmp/foo");
Path p2 = Paths.get(args[0]);
Path p3 = Paths.get(URI.create("file:///Users/joe/FileTest.java"));
```


### **Converting a Path**
You can use three methods to convert the path.  
1. The `toUri` method converts a path to a string that can be opened from a browser.  
   ```java
    Path p1 = Paths.get("/home/logfile");
    System.out.format("%s%n", p1.toUri());
    // Result is file:///home/logfile
    ```
2. The `toAbsolutePath` method converts a path to an absolute path, very helpful when processing user-entered file names.
   ```java
   Path inputPath = Paths.get(args[0]);
   Path fullPath = inputPath.toAbsolutePath();
   ```
3. The `toRealPath` method returns the real path of an existing file. This method performs several operations in one:
    - If `true` is passed to this method and the file system supports symbolic links, this method resolves any symbolic links in the path.
    - If the path is relative, it returns an absolute path.
    - If the path contains any redundant elements, it returns a path with those elements removed.
    ```java
    Path fp = path.toRealPath();
    ```

### **Joining Two Paths**
You can combine paths by using the `resolve` method. You pass in a partial path, which is a path that does not include a root element, and that partial path is appended to the original path. Passing an absolute path to the `resolve` method returns the passed-in path.
```java
Path p1 = Paths.get("C:\\home\\joe\\foo");
System.out.format("%s%n", p1.resolve("bar"));
// Result is C:\home\joe\foo\bar
```


### **Creating a Path Between Two Paths**
The `relativize` method constructs a path originating from the original path and ending at the location specified by the passed-in path. The new path is relative to the original path.
```java
Path p1 = Paths.get("home");
Path p3 = Paths.get("home/sally/bar");
Path p1_to_p3 = p1.relativize(p3);
// Result is sally/bar
Path p3_to_p1 = p3.relativize(p1);
// Result is ../..
```
A relative path cannot be constructed if only one of the paths includes a root element. If both paths include a root element, the capability to construct a relative path is system dependent.


### **Comparing Two Paths**
The `Path` class supports `equals`, enabling you to test two paths for equality. The `startsWith` and `endsWith` methods enable you to test whether a path begins or ends with a particular string.  
```java
Path path = ...;
Path otherPath = ...;
Path beginning = Paths.get("/home");
Path ending = Paths.get("foo");

if (path.equals(otherPath)) {
    // equality logic here
} else if (path.startsWith(beginning)) {
    // path begins with "/home"
} else if (path.endsWith(ending)) {
    // path ends with "foo"
}
```


## File Operations
The `Files` class offers a rich set of static methods for reading, writing, and manipulating files and directories. The Files methods work on instances of `Path` objects.


### **Releasing System Resources**
Neglecting to close a resource can have a negative implication on an application's performance.


### **Atomic Operations**
Several `Files` methods, such as `move`, can perform certain operations atomically in some file systems.

An atomic file operation is an operation that cannot be interrupted or "partially" performed. Either the entire operation is performed or the operation fails. This is important when you have multiple processes operating on the same area of the file system, and you need to guarantee that each process accesses a complete file.


### **Glob**
You can use glob syntax to specify pattern-matching behavior.

A glob pattern is specified as a string and is matched against other strings, such as directory or file names. Glob syntax follows several simple rules:

- An asterisk, *, matches any number of characters (including none).
- Two asterisks, **, works like * but crosses directory boundaries. This syntax is generally used for matching complete paths.
- A question mark, ?, matches exactly one character.
- Braces specify a collection of subpatterns. For example:
  - {sun,moon,stars} matches "sun", "moon", or "stars".
  - {temp*,tmp*} matches all strings beginning with "temp" or "tmp".
- Square brackets convey a set of single characters or, when the hyphen character (-) is used, a range of characters. For example:
  - [aeiou] matches any lowercase vowel.
  - [0-9] matches any digit.
  - [A-Z] matches any uppercase letter.
  - [a-z,A-Z] matches any uppercase or lowercase letter.
- Within the square brackets, *, ?, and \ match themselves.
- All other characters match themselves.
- To match *, ?, or the other special characters, you can escape them by using the backslash character, \. For example: \\ matches a single backslash, and \? matches the question mark.

## Checking a File or Directory
### Verifying the Existence of a File or Directory
Note that `!Files.exists(path)` is not equivalent to `Files.notExists(path)`. When you are testing a file's existence, three results are possible:

- The file is verified to exist.
- The file is verified to not exist.
- The file's status is unknown. This result can occur when the program does not have access to the file.  

If both exists and notExists return false, the existence of the file cannot be verified.

### Checking File Accessibility
Use `isReadable(Path)`, `isWritable(Path)`, and `isExecutable(Path)` methods.

### Checking Whether Two Paths Locate the Same File
Use `isSameFile(Path, Path)`.


## Deleting a File or Directory
The `Files` class provides two deletion methods:
-  `delete(Path)`, throws `NoSuchFileException` if the file does not exist
-  `deleteIfExists(Path)`

## Managing Metadata (File and File Store Attributes)
### Basic File Attributes
Use `Files.readAttributes()` methods.


### POSIX File Permissions
POSIX is a set of IEEE and ISO standards designed to ensure interoperability among different flavors of UNIX.
Besides file owner and group owner, POSIX supports nine file permissions: read, write, and execute permissions for the file owner, members of the same group, and "everyone else."


## Reading, Writing, and Creating Files
### Commonly Used Methods for Small Files
Read/write all bytes/lines in one pass.
- `readAllBytes(Path)`
- `readAllLines(Path, Charset)`
- `write(Path, byte[], OpenOption...)`
- `write(Path, Iterable< extends CharSequence>, Charset, OpenOption...)`


### Buffered I/O Methods for Text Files
Moves data in buffer.
- `newBufferedReader(Path, Charset)`
- `newBufferedWriter(Path, Charset, OpenOption...)`


### Methods for Unbuffered Streams and Interoperable with java.io APIs
Return unbuffered stream to read/write bytes (a character at a time).
- `newInputStream(Path, OpenOption...)`
- `newOutputStream(Path, OpenOption...)`

### Methods for Channels and ByteBuffers
Read a buffer at a time. A SeekableByteChannel is a ByteChannel that has the capability to maintain a position in the channel and to change that position. A SeekableByteChannel also supports truncating the file associated with the channel and querying the file for its size.

The capability to move to different points in the file and then read from or write to that location makes random access of a file possible.
- `newByteChannel(Path, OpenOption...)`
- `newByteChannel(Path, Set<? extends OpenOption>, FileAttribute<?>...)`

### Methods for Creating Regular and Temporary Files
- `createFile(Path, FileAttribute<?>)`
- `createTempFile(String, String, FileAttribute<?>)`

## Links, Symbolic or Otherwise
Hard links are more restrictive than symbolic links, as follows:

- The target of the link must exist.
- Hard links are generally not allowed on directories.
- Hard links are not allowed to cross partitions or volumes. Therefore, they cannot exist across file systems.
- A hard link looks, and behaves, like a regular file, so they can be hard to find.
- A hard link is, for all intents and purposes, the same entity as the original file. They have the same file permissions, time stamps, and so on. All attributes are identical.

Because of these restrictions, hard links are not used as often as symbolic links, but the Path methods work seamlessly with hard links.

### Creating Symbolic Links
`createSymbolicLink(Path, Path, FileAttribute<?>)`

### Creating Hard Links
`createLink(Path, Path)`

### Detecting Symbolic Links
`isSymbolicLink(Path)`

### Finding the Target of a Link
`readSymbolicLink(Path)`

## Other Useful Methods
### Determining MIME Type
File does not only have extension type, but also MIME type.  
`probeContentType(Path)` return MIME type of a file using platform default file type detector. 
Detecting MIME type also depends on the framework or library used, each one may have different implementation to detect MIME type.

## Drawbacks of `java.io.File`
- Many methods didn't throw exceptions when they failed.
- The rename method didn't work consistently across platforms.
- There was no real support for symbolic links.
- More support for metadata was desired.
- Accessing file metadata was inefficient.
- Many of the File methods didn't scale.
- It was not possible to write reliable code that could recursively walk a file tree and respond appropriately if there were circular symbolic links.


# Maven
## Creating Maven Projects
1. Open `pom.xml`.
2. Add `maven-jar-plugin` plugin.
    ```xml
    <plugins>
        <plugin>
            <artifactId>maven-jar-plugin</artifactId>
            <version>3.0.2</version>
            <configuration>
                <manifest>
                    <mainClass>path.to.main.class</mainClass>
                </manifest>
            </configuration>
        </plugin>
    </plugins>
    ```
3. Use `mvn clean install` command to build the program. This will also download all missing plugins and dependencies.

## Unit Testing
1. Open `pom.xml`.
2. Add `junit` dependency.
    ```xml
    <dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.11</version>
            <scope>test</scope>
        </dependency>
    </dependencies>
    ```
3. Test result will be shown when building the program.

### Unit Test Coverage
Unit test coverage is the amount of code covered in the program unit tests.