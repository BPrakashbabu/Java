Here’s a detailed guide on Exception Handling in Java from basic to advanced, including concepts, syntax, and practical scenarios often seen in real-world code and competitive programming.

Exception Handling in Java: Basic to Advanced
1. What is Exception Handling?

Exception Handling lets you manage runtime errors so the normal flow of the program can be maintained. Exceptions are events that disrupt normal program flow.

2. Types of Exceptions
Type	Description	Checked or Unchecked?
Error	Serious system errors (e.g., OutOfMemoryError)	Neither — cannot be handled
Checked Exception	Must be handled or declared (e.g., IOException)	Checked (compile-time)
Unchecked Exception	Runtime exceptions (e.g., NullPointerException)	Unchecked (runtime)
3. Basic Syntax of Exception Handling
try {
    // Code that might throw exception
} catch (ExceptionType e) {
    // Handle exception
} finally {
    // Optional block, always executes
}

4. Example: Basic Exception Handling
public class BasicExceptionExample {
    public static void main(String[] args) {
        try {
            int a = 10 / 0;   // throws ArithmeticException
        } catch (ArithmeticException e) {
            System.out.println("Cannot divide by zero!");
        } finally {
            System.out.println("This block executes regardless of exceptions.");
        }
    }
}


Output:

Cannot divide by zero!
This block executes regardless of exceptions.

5. Multiple Catch Blocks
try {
    // some code
} catch (NullPointerException e) {
    // handle null pointer
} catch (ArrayIndexOutOfBoundsException e) {
    // handle array index exception
} catch (Exception e) {
    // generic handler
}

6. Catching Multiple Exceptions in One Catch Block (Java 7+)
try {
    // code
} catch (IOException | SQLException e) {
    e.printStackTrace();
}

7. Throwing Exceptions

You can throw exceptions explicitly using throw.

public static void checkAge(int age) {
    if (age < 18) {
        throw new IllegalArgumentException("Age must be 18 or older.");
    }
}

8. Declaring Exceptions with throws

When a method can throw a checked exception, you must declare it:

public void readFile() throws IOException {
    // code that may throw IOException
}

9. Custom Exceptions

Create your own exception by extending Exception (checked) or RuntimeException (unchecked).

class MyException extends Exception {
    public MyException(String message) {
        super(message);
    }
}

public class Test {
    public static void check(int num) throws MyException {
        if (num < 0) throw new MyException("Negative number not allowed.");
    }
}

10. Real-Time / Interview Problems
1) Handle Array Out of Bounds
try {
    int[] arr = {1, 2, 3};
    System.out.println(arr[5]);
} catch (ArrayIndexOutOfBoundsException e) {
    System.out.println("Index out of bounds!");
}

2) NullPointerException Handling
try {
    String s = null;
    System.out.println(s.length());
} catch (NullPointerException e) {
    System.out.println("Null string reference!");
}

3) Input Validation with Exception
import java.util.Scanner;

public class InputValidation {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int num = 0;
        while (true) {
            System.out.print("Enter an integer: ");
            try {
                num = Integer.parseInt(sc.nextLine());
                break;
            } catch (NumberFormatException e) {
                System.out.println("Invalid number, try again.");
            }
        }
        System.out.println("You entered: " + num);
    }
}

4) Using try-with-resources (Java 7+)

Automatically closes resources implementing AutoCloseable.

try (Scanner sc = new Scanner(System.in)) {
    System.out.println("Enter input:");
    String input = sc.nextLine();
    System.out.println("Input: " + input);
} catch (Exception e) {
    e.printStackTrace();
}

11. Best Practices

Catch the most specific exception first.

Avoid empty catch blocks.

Use finally for cleanup code.

Prefer try-with-resources for closing resources.

Use custom exceptions for better error reporting.

Document exceptions thrown by your methods.

12. Advanced: Exception Chaining
try {
    // code
} catch (IOException e) {
    throw new RuntimeException("Failed to read file", e);  // chaining cause
}

13. Common Exceptions and when they occur
Exception	When does it occur?
ArithmeticException	Divide by zero
NullPointerException	Calling method/field on null object
ArrayIndexOutOfBoundsException	Access invalid index in array
ClassCastException	Invalid casting between classes
IOException	Input/output failure
FileNotFoundException	File missing when trying to open it
14. Sample Program Combining Concepts
import java.util.Scanner;

public class ExceptionHandlingDemo {

    public static void validateAge(int age) throws IllegalArgumentException {
        if (age < 18) {
            throw new IllegalArgumentException("Age must be 18 or above.");
        }
    }

    public static void main(String[] args) {
        try (Scanner scanner = new Scanner(System.in)) {
            System.out.print("Enter age: ");
            int age = Integer.parseInt(scanner.nextLine());

            validateAge(age);
            System.out.println("Age is valid: " + age);

        } catch (IllegalArgumentException e) {
            System.out.println("Validation Error: " + e.getMessage());
        } catch (NumberFormatException e) {
            System.out.println("Please enter a valid number.");
        } catch (Exception e) {
            System.out.println("An unexpected error occurred.");
            e.printStackTrace();
        } finally {
            System.out.println("Program ended.");
        }
    }
}
