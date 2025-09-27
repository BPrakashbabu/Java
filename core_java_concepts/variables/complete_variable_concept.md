1. Basic Variables in Java

Variables in Java are used to store data. Every variable has a data type (like int, double, String, etc.), a name (or identifier), and a value.

Example:
public class BasicVariables {
    public static void main(String[] args) {
        // Declaring and initializing variables
        int age = 25;           // integer variable
        double price = 19.99;    // double variable (for decimal values)
        char grade = 'A';        // character variable (single character)
        String name = "John";    // String variable (for text)

        // Outputting the values
        System.out.println("Name: " + name);
        System.out.println("Age: " + age);
        System.out.println("Price: $" + price);
        System.out.println("Grade: " + grade);
    }
}


Explanation:

int is used for integers (whole numbers).

double is used for floating-point numbers (decimal values).

char is used for a single character.

String is used for a sequence of characters (text).

2. Variable Scope

In Java, variables can be local or instance variables.

Example:
public class VariableScope {
    int instanceVar = 10;  // Instance variable

    public void method() {
        int localVar = 20;  // Local variable
        System.out.println("Local Variable: " + localVar);
        System.out.println("Instance Variable: " + instanceVar);
    }

    public static void main(String[] args) {
        VariableScope obj = new VariableScope();
        obj.method();
    }
}


Explanation:

Instance variable: Belongs to an instance of the class and can be accessed anywhere within the class.

Local variable: Declared within a method and can only be accessed inside that method.

3. Constants (Final Variables)

In Java, a variable can be declared as a constant using the final keyword. Once assigned a value, it cannot be changed.

Example:
public class ConstantsExample {
    public static void main(String[] args) {
        final double PI = 3.14159; // Constant value
        System.out.println("Value of PI: " + PI);

        // Uncommenting the following line will cause an error
        // PI = 3.14;  // Error: Cannot assign a value to a final variable
    }
}


Explanation:

final makes a variable constant (its value cannot be reassigned once set).

4. Type Casting (Implicit and Explicit)

Sometimes, Java needs to convert one data type to another. This is called type casting.

Example: Implicit Casting (Widening)
public class ImplicitCasting {
    public static void main(String[] args) {
        int intValue = 100;
        double doubleValue = intValue;  // Implicit casting (int to double)
        
        System.out.println("Double value: " + doubleValue);
    }
}

Example: Explicit Casting (Narrowing)
public class ExplicitCasting {
    public static void main(String[] args) {
        double doubleValue = 99.99;
        int intValue = (int) doubleValue;  // Explicit casting (double to int)
        
        System.out.println("Int value: " + intValue);  // It will lose the decimal part
    }
}


Explanation:

Implicit casting: Java automatically converts a smaller type to a larger type (e.g., int to double).

Explicit casting: When converting from a larger type to a smaller type, you need to explicitly cast it (e.g., double to int).

5. Array Variables

In Java, arrays are a type of variable that can hold multiple values of the same type.

Example:
public class ArrayExample {
    public static void main(String[] args) {
        int[] numbers = {1, 2, 3, 4, 5};  // Array initialization

        System.out.println("First number: " + numbers[0]);
        System.out.println("Last number: " + numbers[4]);
    }
}


Explanation:

An array is a collection of elements of the same type. The size of the array is fixed when it's created.

6. Variable Arguments (Varargs)

In Java, you can pass a variable number of arguments to a method using varargs.

Example:
public class VarargsExample {
    public static void printNumbers(int... numbers) {
        for (int num : numbers) {
            System.out.println(num);
        }
    }

    public static void main(String[] args) {
        printNumbers(1, 2, 3);  // Passing 3 numbers
        printNumbers(10, 20, 30, 40, 50);  // Passing 5 numbers
    }
}


Explanation:

int... numbers is used to pass a variable number of arguments (varargs) to the method. The arguments are stored as an array inside the method.

7. Wrapper Classes

In Java, each primitive data type has a corresponding wrapper class that allows you to work with the primitive values as objects. For example, int has Integer, char has Character, etc.

Example:
public class WrapperClasses {
    public static void main(String[] args) {
        int primitiveInt = 100;
        
        // Converting primitive int to Integer object
        Integer wrappedInt = Integer.valueOf(primitiveInt);

        System.out.println("Primitive int: " + primitiveInt);
        System.out.println("Wrapped Integer: " + wrappedInt);
    }
}


Explanation:

Wrapper classes provide utility methods for working with primitive types as objects. For instance, Integer.valueOf(int) converts an int into an Integer object.

8. Advanced: Using var (Java 10+)

Since Java 10, you can use var for local variables, where the compiler will infer the type.

Example:
public class VarKeywordExample {
    public static void main(String[] args) {
        var name = "John";     // String type inferred
        var age = 30;          // int type inferred
        var price = 19.99;     // double type inferred

        System.out.println("Name: " + name);
        System.out.println("Age: " + age);
        System.out.println("Price: " + price);
    }
}


Explanation:

var allows Java to infer the type based on the value assigned to the variable. It’s only used for local variables (within methods), not for fields or method parameters.

Conclusion

This program covered the basics of variables in Java, including:

Primitive and reference types

Variable scope (local vs instance)

Constants (final)

Type casting (implicit and explicit)

Arrays and varargs

Wrapper classes and var in modern Java
