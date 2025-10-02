Let’s go step-by-step through Serialization in Java from basic to advanced concepts.

Serialization in Java — Basic to Advanced
1. What is Serialization?

Serialization is the process of converting an object into a byte stream.

This byte stream can be saved to a file, sent over a network, or stored in a database.

The purpose is to save the object's state so it can be recreated later.

2. What is Deserialization?

The reverse process of serialization.

It converts the byte stream back into a copy of the original object.

3. Why Serialization?

To persist an object’s state.

To send objects over the network (e.g., RMI, sockets).

To store objects in files or databases.

4. Basic Requirements for Serialization

A class must implement the java.io.Serializable interface.

This interface is a marker interface (it has no methods).

Example:

import java.io.Serializable;

public class Employee implements Serializable {
    private int id;
    private String name;
    
    public Employee(int id, String name) {
        this.id = id;
        this.name = name;
    }

    // getters and setters
}

5. Serialization Example (Basic)
import java.io.*;

public class SerializeDemo {
    public static void main(String[] args) {
        Employee emp = new Employee(101, "John");

        try (ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("employee.ser"))) {
            oos.writeObject(emp);
            System.out.println("Serialization done");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

6. Deserialization Example (Basic)
import java.io.*;

public class DeserializeDemo {
    public static void main(String[] args) {
        try (ObjectInputStream ois = new ObjectInputStream(new FileInputStream("employee.ser"))) {
            Employee emp = (Employee) ois.readObject();
            System.out.println("Employee ID: " + emp.getId());
            System.out.println("Employee Name: " + emp.getName());
        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
}

7. Important Points

transient keyword: Use this keyword to prevent serialization of a variable.

private transient int salary;


serialVersionUID: It is used for version control of a Serializable class.

private static final long serialVersionUID = 1L;


If serialVersionUID does not match during deserialization, it throws InvalidClassException.

8. Customizing Serialization

You can customize the serialization process by implementing two special methods in your class:

private void writeObject(ObjectOutputStream oos) throws IOException {
    // custom code before serialization
    oos.defaultWriteObject();  // default serialization
    // custom code after serialization
}

private void readObject(ObjectInputStream ois) throws IOException, ClassNotFoundException {
    // custom code before deserialization
    ois.defaultReadObject();  // default deserialization
    // custom code after deserialization
}

9. Handling Inheritance

If a superclass is not Serializable, its no-arg constructor is called during deserialization.

Subclasses can still implement Serializable independently.

10. Externalizable Interface

Extends Serializable but requires you to override two methods: writeExternal() and readExternal().

Gives full control over serialization.

public class Employee implements Externalizable {
    private int id;
    private String name;

    public Employee() {
        // mandatory no-arg constructor
    }

    public void writeExternal(ObjectOutput out) throws IOException {
        out.writeInt(id);
        out.writeObject(name);
    }

    public void readExternal(ObjectInput in) throws IOException, ClassNotFoundException {
        id = in.readInt();
        name = (String) in.readObject();
    }
}

11. Serialization Proxies

Used to improve serialization security and maintain class invariants.

The idea is to use a private static nested class as a proxy to handle serialization.

12. Common Serialization Issues

Changing class structure breaks deserialization unless managed via serialVersionUID.

Transient fields are skipped.

Circular references are handled automatically by Java serialization.

13. Advanced: Serialization Filtering

Since Java 9, you can apply filters to control what gets deserialized, improving security.