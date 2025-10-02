Here’s a comprehensive guide to File I/O (Input and Output) in Java, starting from basic to advanced concepts. I’ll include code examples, explanations, and best practices.

🟢 1. Basics of File I/O in Java

Java uses the java.io and java.nio packages for file I/O.

✅ Reading a File (Basic)
Using FileReader and BufferedReader
import java.io.*;

public class ReadFileExample {
    public static void main(String[] args) {
        try (BufferedReader br = new BufferedReader(new FileReader("example.txt"))) {
            String line;
            while ((line = br.readLine()) != null) {
                System.out.println(line);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

✅ Writing to a File
Using FileWriter and BufferedWriter
import java.io.*;

public class WriteFileExample {
    public static void main(String[] args) {
        try (BufferedWriter bw = new BufferedWriter(new FileWriter("output.txt"))) {
            bw.write("Hello, Java File I/O!");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

🟡 2. Intermediate File I/O
✅ File Handling
import java.io.File;

public class FileHandling {
    public static void main(String[] args) {
        File file = new File("example.txt");

        if (file.exists()) {
            System.out.println("File name: " + file.getName());
            System.out.println("Path: " + file.getAbsolutePath());
            System.out.println("Readable: " + file.canRead());
            System.out.println("Writable: " + file.canWrite());
            System.out.println("Size: " + file.length());
        } else {
            System.out.println("The file does not exist.");
        }
    }
}

✅ Reading and Writing Binary Files
Example: Copying a binary file
import java.io.*;

public class CopyBinaryFile {
    public static void main(String[] args) {
        try (FileInputStream in = new FileInputStream("source.jpg");
             FileOutputStream out = new FileOutputStream("copy.jpg")) {

            byte[] buffer = new byte[1024];
            int bytesRead;

            while ((bytesRead = in.read(buffer)) != -1) {
                out.write(buffer, 0, bytesRead);
            }

            System.out.println("File copied.");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

✅ Object Serialization
import java.io.*;

class Person implements Serializable {
    String name;
    int age;
    Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}

public class SerializeDemo {
    public static void main(String[] args) {
        Person p = new Person("Alice", 30);

        // Serialization
        try (ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("person.ser"))) {
            oos.writeObject(p);
        } catch (IOException e) {
            e.printStackTrace();
        }

        // Deserialization
        try (ObjectInputStream ois = new ObjectInputStream(new FileInputStream("person.ser"))) {
            Person person = (Person) ois.readObject();
            System.out.println("Name: " + person.name + ", Age: " + person.age);
        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
}

🔵 3. Advanced File I/O (NIO)
✅ Java NIO (New I/O)

Java NIO (in java.nio.file) is more efficient for handling large files.

Reading All Lines (NIO)
import java.nio.file.*;
import java.io.IOException;
import java.util.List;

public class NIOReadExample {
    public static void main(String[] args) {
        try {
            List<String> lines = Files.readAllLines(Paths.get("example.txt"));
            for (String line : lines) {
                System.out.println(line);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

Writing Using Files.write()
import java.nio.file.*;
import java.io.IOException;
import java.util.Arrays;

public class NIOWriteExample {
    public static void main(String[] args) {
        try {
            Path path = Paths.get("output.txt");
            Files.write(path, Arrays.asList("Line 1", "Line 2"), StandardOpenOption.CREATE);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

✅ Walking a Directory Tree
import java.io.IOException;
import java.nio.file.*;

public class WalkFileTreeExample {
    public static void main(String[] args) throws IOException {
        Path startPath = Paths.get(".");

        Files.walk(startPath)
             .filter(Files::isRegularFile)
             .forEach(System.out::println);
    }
}

✅ Watch Service (Watching File Changes)
import java.nio.file.*;

public class WatchDirectory {
    public static void main(String[] args) throws Exception {
        WatchService watchService = FileSystems.getDefault().newWatchService();
        Path path = Paths.get(".");

        path.register(watchService, StandardWatchEventKinds.ENTRY_CREATE,
                      StandardWatchEventKinds.ENTRY_DELETE,
                      StandardWatchEventKinds.ENTRY_MODIFY);

        System.out.println("Watching directory: " + path);

        WatchKey key;
        while ((key = watchService.take()) != null) {
            for (WatchEvent<?> event : key.pollEvents()) {
                System.out.println("Event kind: " + event.kind()
                    + ". File affected: " + event.context() + ".");
            }
            key.reset();
        }
    }
}

🧠 Best Practices

Always close streams (use try-with-resources).

Use buffered streams for performance.

Prefer NIO for modern applications.

Handle exceptions gracefully.

Avoid hardcoding file paths.

📚 Useful Classes Summary
Class	Use Case
File, Path	File metadata and paths
FileReader, FileWriter	Character-based I/O
BufferedReader, BufferedWriter	Efficient character I/O
FileInputStream, FileOutputStream	Byte-based I/O
ObjectInputStream, ObjectOutputStream	Serialization
Files, Paths (NIO)	Modern file handling
WatchService	Directory monitoring