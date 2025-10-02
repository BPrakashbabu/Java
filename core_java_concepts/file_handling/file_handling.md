Here's a comprehensive guide to File Handling in Java, covering everything from basic to advanced concepts. You'll learn how to create, read, write, delete files, and use modern Java features like NIO, streams, and watch services.

🟢 1. Basic File Handling
✅ Creating a File
import java.io.File;
import java.io.IOException;

public class CreateFile {
    public static void main(String[] args) {
        File file = new File("sample.txt");
        try {
            if (file.createNewFile()) {
                System.out.println("File created: " + file.getName());
            } else {
                System.out.println("File already exists.");
            }
        } catch (IOException e) {
            System.out.println("An error occurred.");
            e.printStackTrace();
        }
    }
}

✅ Writing to a File
import java.io.FileWriter;
import java.io.IOException;

public class WriteToFile {
    public static void main(String[] args) {
        try (FileWriter writer = new FileWriter("sample.txt")) {
            writer.write("Hello, Java File Handling!");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

✅ Reading from a File
import java.io.File;
import java.io.FileNotFoundException;
import java.util.Scanner;

public class ReadFromFile {
    public static void main(String[] args) {
        try {
            File file = new File("sample.txt");
            Scanner reader = new Scanner(file);
            while (reader.hasNextLine()) {
                System.out.println(reader.nextLine());
            }
            reader.close();
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        }
    }
}

✅ Deleting a File
import java.io.File;

public class DeleteFile {
    public static void main(String[] args) {
        File file = new File("sample.txt");
        if (file.delete()) {
            System.out.println("Deleted the file: " + file.getName());
        } else {
            System.out.println("Failed to delete the file.");
        }
    }
}

🟡 2. Intermediate File Handling
✅ Using BufferedWriter and BufferedReader
import java.io.*;

public class BufferedFileIO {
    public static void main(String[] args) {
        String filename = "buffered.txt";

        // Writing
        try (BufferedWriter writer = new BufferedWriter(new FileWriter(filename))) {
            writer.write("This is a buffered write.\nLine two.");
        } catch (IOException e) {
            e.printStackTrace();
        }

        // Reading
        try (BufferedReader reader = new BufferedReader(new FileReader(filename))) {
            String line;
            while ((line = reader.readLine()) != null) {
                System.out.println(line);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

✅ Copying Files (Binary Files)
import java.io.*;

public class CopyFile {
    public static void main(String[] args) {
        try (FileInputStream in = new FileInputStream("source.jpg");
             FileOutputStream out = new FileOutputStream("copy.jpg")) {

            byte[] buffer = new byte[1024];
            int length;
            while ((length = in.read(buffer)) > 0) {
                out.write(buffer, 0, length);
            }

            System.out.println("File copied.");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

✅ List Files in a Directory
import java.io.File;

public class ListDirectoryFiles {
    public static void main(String[] args) {
        File folder = new File(".");
        File[] listOfFiles = folder.listFiles();

        for (File file : listOfFiles) {
            if (file.isFile()) {
                System.out.println("File: " + file.getName());
            } else if (file.isDirectory()) {
                System.out.println("Directory: " + file.getName());
            }
        }
    }
}

🔵 3. Advanced File Handling (NIO)

Java NIO (java.nio.file) provides more efficient and flexible file handling.

✅ Reading All Lines with NIO
import java.nio.file.*;
import java.io.IOException;
import java.util.List;

public class NIORead {
    public static void main(String[] args) {
        try {
            List<String> lines = Files.readAllLines(Paths.get("sample.txt"));
            lines.forEach(System.out::println);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

✅ Writing with NIO
import java.nio.file.*;
import java.io.IOException;
import java.util.Arrays;

public class NIOWrite {
    public static void main(String[] args) {
        Path path = Paths.get("nio-output.txt");
        try {
            Files.write(path, Arrays.asList("Line 1", "Line 2"), StandardOpenOption.CREATE);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

✅ Walking a Directory Tree
import java.io.IOException;
import java.nio.file.*;

public class DirectoryWalker {
    public static void main(String[] args) throws IOException {
        Path path = Paths.get(".");
        Files.walk(path, 2)
             .filter(Files::isRegularFile)
             .forEach(System.out::println);
    }
}

✅ WatchService – Watching File Changes
import java.io.IOException;
import java.nio.file.*;

public class FileWatcher {
    public static void main(String[] args) throws IOException, InterruptedException {
        WatchService watchService = FileSystems.getDefault().newWatchService();
        Path path = Paths.get(".");
        path.register(watchService,
                      StandardWatchEventKinds.ENTRY_CREATE,
                      StandardWatchEventKinds.ENTRY_DELETE,
                      StandardWatchEventKinds.ENTRY_MODIFY);

        System.out.println("Watching directory: " + path.toAbsolutePath());

        WatchKey key;
        while ((key = watchService.take()) != null) {
            for (WatchEvent<?> event : key.pollEvents()) {
                System.out.println("Event kind: " + event.kind() +
                                   ". File affected: " + event.context() + ".");
            }
            key.reset();
        }
    }
}

✅ File Permissions and Attributes (Advanced)
import java.io.IOException;
import java.nio.file.*;
import java.nio.file.attribute.BasicFileAttributes;

public class FileAttributes {
    public static void main(String[] args) {
        try {
            Path file = Paths.get("sample.txt");
            BasicFileAttributes attr = Files.readAttributes(file, BasicFileAttributes.class);
            System.out.println("Creation Time: " + attr.creationTime());
            System.out.println("Last Access Time: " + attr.lastAccessTime());
            System.out.println("Size: " + attr.size() + " bytes");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

🧠 Best Practices

Always use try-with-resources to auto-close streams.

Prefer Buffered streams for performance.

Use NIO for new projects and large-scale file operations.

Handle exceptions carefully to avoid data corruption.

Avoid hardcoding file paths — use Paths.get() and File.separator.