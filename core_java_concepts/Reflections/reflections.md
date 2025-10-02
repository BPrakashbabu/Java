Here's a full guide to Reflection in Java, from basic concepts to advanced usage, including code examples and best practices.

🔍 What Is Java Reflection?

Java Reflection is a powerful API in the java.lang.reflect package that allows you to:

Inspect classes, methods, constructors, fields, annotations at runtime

Access private members

Create instances and invoke methods dynamically

✅ Use cases:

Frameworks (Spring, Hibernate)

IDEs, debuggers

Testing frameworks (JUnit, Mockito)

Serialization/deserialization (Jackson, Gson)

🟢 1. Basic Reflection
✅ Getting Class Object
// Option 1: Using Class.forName()
Class<?> cls = Class.forName("java.lang.String");

// Option 2: Using .class
Class<?> cls2 = String.class;

// Option 3: Using object.getClass()
String str = "Hello";
Class<?> cls3 = str.getClass();

✅ Get Class Name & Modifiers
System.out.println("Class Name: " + cls.getName());
System.out.println("Is Interface? " + cls.isInterface());
System.out.println("Superclass: " + cls.getSuperclass());

🟡 2. Inspecting Members
✅ Fields (Variables)
import java.lang.reflect.Field;

class Person {
    public String name;
    private int age;
}

public class FieldExample {
    public static void main(String[] args) throws Exception {
        Class<?> cls = Person.class;
        Field[] fields = cls.getDeclaredFields();

        for (Field field : fields) {
            System.out.println("Field: " + field.getName() + " | Type: " + field.getType());
        }
    }
}

✅ Methods
import java.lang.reflect.Method;

public class MethodExample {
    public static void main(String[] args) {
        Class<?> cls = String.class;

        Method[] methods = cls.getDeclaredMethods();
        for (Method method : methods) {
            System.out.println("Method: " + method.getName());
        }
    }
}

✅ Constructors
import java.lang.reflect.Constructor;

public class ConstructorExample {
    public static void main(String[] args) {
        Class<?> cls = String.class;

        Constructor<?>[] constructors = cls.getConstructors();
        for (Constructor<?> constructor : constructors) {
            System.out.println("Constructor: " + constructor);
        }
    }
}

🟠 3. Manipulating Objects
✅ Creating an Object with Reflection
class Animal {
    public Animal() {
        System.out.println("Animal created!");
    }
}

public class CreateObject {
    public static void main(String[] args) throws Exception {
        Class<?> cls = Animal.class;
        Object obj = cls.getDeclaredConstructor().newInstance();  // Creates instance
    }
}

✅ Accessing Private Fields
class Secret {
    private String code = "TOP_SECRET";
}

public class AccessPrivateField {
    public static void main(String[] args) throws Exception {
        Secret secret = new Secret();
        Class<?> cls = secret.getClass();

        Field field = cls.getDeclaredField("code");
        field.setAccessible(true);  // Bypass private access
        String value = (String) field.get(secret);

        System.out.println("Secret Code: " + value);
    }
}

✅ Invoking Methods Dynamically
class Calculator {
    public int add(int a, int b) {
        return a + b;
    }
}

public class InvokeMethod {
    public static void main(String[] args) throws Exception {
        Calculator calc = new Calculator();
        Method method = Calculator.class.getMethod("add", int.class, int.class);

        int result = (int) method.invoke(calc, 10, 20);
        System.out.println("Result: " + result);  // 30
    }
}

🔵 4. Advanced Reflection
✅ Annotations and Reflection
import java.lang.annotation.*;
import java.lang.reflect.*;

@Retention(RetentionPolicy.RUNTIME)
@interface Info {
    String author();
}

@Info(author = "John")
class Demo {}

public class AnnotationExample {
    public static void main(String[] args) {
        Class<?> cls = Demo.class;
        if (cls.isAnnotationPresent(Info.class)) {
            Info info = cls.getAnnotation(Info.class);
            System.out.println("Author: " + info.author());
        }
    }
}

✅ Working with Generic Types (Reflection + Generics)
import java.lang.reflect.ParameterizedType;
import java.lang.reflect.Type;

class Box<T> {}

class StringBox extends Box<String> {}

public class GenericTypeExample {
    public static void main(String[] args) {
        Type superClass = StringBox.class.getGenericSuperclass();
        if (superClass instanceof ParameterizedType) {
            Type[] typeArgs = ((ParameterizedType) superClass).getActualTypeArguments();
            System.out.println("Generic Type: " + typeArgs[0]);  // class java.lang.String
        }
    }
}

✅ Dynamic Proxy (Advanced)

Use case: AOP, intercepting method calls (used heavily in Spring)

import java.lang.reflect.*;

interface Service {
    void serve();
}

class RealService implements Service {
    public void serve() {
        System.out.println("Real Service Called");
    }
}

public class DynamicProxyExample {
    public static void main(String[] args) {
        Service realService = new RealService();

        Service proxy = (Service) Proxy.newProxyInstance(
            Service.class.getClassLoader(),
            new Class<?>[]{Service.class},
            (proxyObj, method, methodArgs) -> {
                System.out.println("Before Method");
                Object result = method.invoke(realService, methodArgs);
                System.out.println("After Method");
                return result;
            }
        );

        proxy.serve();
    }
}

🚨 Reflection Limitations & Risks
Limitation	Explanation
Performance Overhead	Slower than direct method calls
Security Risk	Can access private data
Breaks Encapsulation	Bypasses access modifiers
Compile-time Safety is Lost	Errors may appear only at runtime
✅ Best Practices

Avoid excessive reflection — prefer direct calls where possible.

Cache reflective results if used repeatedly.

Never use reflection to bypass security or business logic.

Use annotations + reflection for meta-programming and frameworks.

📚 Summary: Reflection Capabilities
Feature	API Used
Get class info	Class<?> cls = Class.forName()
Access fields	Field field = cls.getDeclaredField()
Invoke methods	method.invoke(obj, args...)
Create instances	cls.getDeclaredConstructor().newInstance()
Access private members	field.setAccessible(true)
Read annotations	cls.getAnnotation(MyAnnotation.class)
Work with generics	ParameterizedType
Create proxies	Here's a full guide to Reflection in Java, from basic concepts to advanced usage, including code examples and best practices.

🔍 What Is Java Reflection?

Java Reflection is a powerful API in the java.lang.reflect package that allows you to:

Inspect classes, methods, constructors, fields, annotations at runtime

Access private members

Create instances and invoke methods dynamically

✅ Use cases:

Frameworks (Spring, Hibernate)

IDEs, debuggers

Testing frameworks (JUnit, Mockito)

Serialization/deserialization (Jackson, Gson)

🟢 1. Basic Reflection
✅ Getting Class Object
// Option 1: Using Class.forName()
Class<?> cls = Class.forName("java.lang.String");

// Option 2: Using .class
Class<?> cls2 = String.class;

// Option 3: Using object.getClass()
String str = "Hello";
Class<?> cls3 = str.getClass();

✅ Get Class Name & Modifiers
System.out.println("Class Name: " + cls.getName());
System.out.println("Is Interface? " + cls.isInterface());
System.out.println("Superclass: " + cls.getSuperclass());

🟡 2. Inspecting Members
✅ Fields (Variables)
import java.lang.reflect.Field;

class Person {
    public String name;
    private int age;
}

public class FieldExample {
    public static void main(String[] args) throws Exception {
        Class<?> cls = Person.class;
        Field[] fields = cls.getDeclaredFields();

        for (Field field : fields) {
            System.out.println("Field: " + field.getName() + " | Type: " + field.getType());
        }
    }
}

✅ Methods
import java.lang.reflect.Method;

public class MethodExample {
    public static void main(String[] args) {
        Class<?> cls = String.class;

        Method[] methods = cls.getDeclaredMethods();
        for (Method method : methods) {
            System.out.println("Method: " + method.getName());
        }
    }
}

✅ Constructors
import java.lang.reflect.Constructor;

public class ConstructorExample {
    public static void main(String[] args) {
        Class<?> cls = String.class;

        Constructor<?>[] constructors = cls.getConstructors();
        for (Constructor<?> constructor : constructors) {
            System.out.println("Constructor: " + constructor);
        }
    }
}

🟠 3. Manipulating Objects
✅ Creating an Object with Reflection
class Animal {
    public Animal() {
        System.out.println("Animal created!");
    }
}

public class CreateObject {
    public static void main(String[] args) throws Exception {
        Class<?> cls = Animal.class;
        Object obj = cls.getDeclaredConstructor().newInstance();  // Creates instance
    }
}

✅ Accessing Private Fields
class Secret {
    private String code = "TOP_SECRET";
}

public class AccessPrivateField {
    public static void main(String[] args) throws Exception {
        Secret secret = new Secret();
        Class<?> cls = secret.getClass();

        Field field = cls.getDeclaredField("code");
        field.setAccessible(true);  // Bypass private access
        String value = (String) field.get(secret);

        System.out.println("Secret Code: " + value);
    }
}

✅ Invoking Methods Dynamically
class Calculator {
    public int add(int a, int b) {
        return a + b;
    }
}

public class InvokeMethod {
    public static void main(String[] args) throws Exception {
        Calculator calc = new Calculator();
        Method method = Calculator.class.getMethod("add", int.class, int.class);

        int result = (int) method.invoke(calc, 10, 20);
        System.out.println("Result: " + result);  // 30
    }
}

🔵 4. Advanced Reflection
✅ Annotations and Reflection
import java.lang.annotation.*;
import java.lang.reflect.*;

@Retention(RetentionPolicy.RUNTIME)
@interface Info {
    String author();
}

@Info(author = "John")
class Demo {}

public class AnnotationExample {
    public static void main(String[] args) {
        Class<?> cls = Demo.class;
        if (cls.isAnnotationPresent(Info.class)) {
            Info info = cls.getAnnotation(Info.class);
            System.out.println("Author: " + info.author());
        }
    }
}

✅ Working with Generic Types (Reflection + Generics)
import java.lang.reflect.ParameterizedType;
import java.lang.reflect.Type;

class Box<T> {}

class StringBox extends Box<String> {}

public class GenericTypeExample {
    public static void main(String[] args) {
        Type superClass = StringBox.class.getGenericSuperclass();
        if (superClass instanceof ParameterizedType) {
            Type[] typeArgs = ((ParameterizedType) superClass).getActualTypeArguments();
            System.out.println("Generic Type: " + typeArgs[0]);  // class java.lang.String
        }
    }
}

✅ Dynamic Proxy (Advanced)

Use case: AOP, intercepting method calls (used heavily in Spring)

import java.lang.reflect.*;

interface Service {
    void serve();
}

class RealService implements Service {
    public void serve() {
        System.out.println("Real Service Called");
    }
}

public class DynamicProxyExample {
    public static void main(String[] args) {
        Service realService = new RealService();

        Service proxy = (Service) Proxy.newProxyInstance(
            Service.class.getClassLoader(),
            new Class<?>[]{Service.class},
            (proxyObj, method, methodArgs) -> {
                System.out.println("Before Method");
                Object result = method.invoke(realService, methodArgs);
                System.out.println("After Method");
                return result;
            }
        );

        proxy.serve();
    }
}

🚨 Reflection Limitations & Risks
Limitation	Explanation
Performance Overhead	Slower than direct method calls
Security Risk	Can access private data
Breaks Encapsulation	Bypasses access modifiers
Compile-time Safety is Lost	Errors may appear only at runtime
✅ Best Practices

Avoid excessive reflection — prefer direct calls where possible.

Cache reflective results if used repeatedly.

Never use reflection to bypass security or business logic.

Use annotations + reflection for meta-programming and frameworks.

📚 Summary: Reflection Capabilities
Feature	API Used
Get class info	Class<?> cls = Class.forName()
Access fields	Field field = cls.getDeclaredField()
Invoke methods	method.invoke(obj, args...)
Create instances	cls.getDeclaredConstructor().newInstance()
Access private members	field.setAccessible(true)
Read annotations	cls.getAnnotation(MyAnnotation.class)
Work with generics	ParameterizedType
Create proxies	Proxy.newProxyInstance()