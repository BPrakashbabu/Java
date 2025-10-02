Let's explore Java Data Types from basic to advanced, including:

Primitive data types

Non-primitive (reference) data types

Type conversions

Wrapper classes

Advanced usage and memory details

🌱 1. What is a Data Type?

In Java, a data type defines the type of data a variable can hold, like integers, decimals, characters, etc.

🧱 2. Primitive Data Types

Java has 8 primitive data types — these are built-in and not objects.

Data Type	Size	Default	Description	Example
byte	1 byte (8 bits)	0	Small integers (-128 to 127)	byte b = 100;
short	2 bytes	0	Medium integers	short s = 1000;
int	4 bytes	0	Standard integers	int age = 25;
long	8 bytes	0L	Large integers	long l = 123456L;
float	4 bytes	0.0f	Decimal values (less precise)	float f = 3.14f;
double	8 bytes	0.0d	Decimal (more precise)	double d = 3.14;
char	2 bytes	'\u0000'	Single character	char c = 'A';
boolean	1 bit (JVM dependent)	false	true/false value	boolean b = true;
Example: Using All Primitive Types
public class PrimitiveTypes {
    public static void main(String[] args) {
        byte b = 127;
        short s = 32000;
        int i = 100000;
        long l = 1000000000L;
        float f = 5.75f;
        double d = 19.99;
        char c = 'J';
        boolean bool = true;

        System.out.println("byte: " + b);
        System.out.println("short: " + s);
        System.out.println("int: " + i);
        System.out.println("long: " + l);
        System.out.println("float: " + f);
        System.out.println("double: " + d);
        System.out.println("char: " + c);
        System.out.println("boolean: " + bool);
    }
}

📦 3. Non-Primitive (Reference) Data Types

These are not built-in types, but objects or class references:

Type	Description
String	Represents a sequence of characters
Arrays	Collection of fixed-size elements
Classes	User-defined data types
Interfaces	Contracts for class behaviors
Enums	Constants
Collections	Lists, Sets, Maps (from java.util)
Example: Reference Types
public class ReferenceTypes {
    public static void main(String[] args) {
        String name = "Java";
        int[] numbers = {1, 2, 3};

        System.out.println("String: " + name);
        System.out.println("Array element: " + numbers[0]);
    }
}

🔁 4. Type Casting (Conversion)
✅ Widening (Implicit Conversion)

Smaller to larger type (no data loss)

int a = 10;
double b = a; // int -> double

⚠️ Narrowing (Explicit Conversion)

Larger to smaller type (can lose data)

double x = 10.5;
int y = (int) x; // double -> int

🎁 5. Wrapper Classes (Advanced Feature)

Each primitive type has a corresponding object type, used in collections, generics, etc.

Primitive	Wrapper Class
byte	Byte
short	Short
int	Integer
long	Long
float	Float
double	Double
char	Character
boolean	Boolean
Example: Autoboxing & Unboxing
public class WrapperExample {
    public static void main(String[] args) {
        int a = 100;
        Integer obj = a; // Autoboxing (int to Integer)

        int b = obj;     // Unboxing (Integer to int)
        System.out.println("Value: " + b);
    }
}

🧠 6. var Keyword (Java 10+)

Introduces type inference for local variables.

public class VarExample {
    public static void main(String[] args) {
        var num = 50;         // Automatically inferred as int
        var text = "Java";    // Inferred as String
        System.out.println(num + " - " + text);
    }
}


⚠️ Only usable inside methods — not for instance variables or method parameters.

🗂️ 7. Data Type Ranges & Sizes
Type	Size	   Min Value	Max Value
byte	8-bit	   -128	             127
short	16-bit	   -32,768	         32,767
int   	32-bit	  -2,147,483,648	2,147,483,647
long	64-bit  	-9.2e18         	9.2e18
float	32-bit	      ~±3.4e38	       ~±3.4e38
double	64-bit      	~±1.8e308	   ~±1.8e308
char	16-bit	      '\u0000'      	'\uffff' (0 to 65535)
boolean	JVM-defined	     false	            true
⚙️ 8. Memory & Performance Considerations

Primitive types are faster and stored on the stack.

Reference types (objects) are stored in the heap.

Always use primitives when performance or memory is critical.

Use wrapper classes when objects are needed (e.g., in collections like ArrayList<Integer>).

🧰 9. Utilities from Sub-packages
java.lang (Core data types)

Integer, Double, Boolean, Character – wrapper utilities

Math – mathematical operations on data types

String – for text processing

java.util

Arrays, ArrayList, HashMap – use reference types

Generic types require wrapper classes: ArrayList<Integer>, not int

java.text

Formatting numbers/dates into strings using proper formats.

✅ Summary
Level	Topics Covered
Basic	Primitive types (int, char, boolean, etc.)
Intermediate	Reference types (String, Arrays, Classes)
Advanced	Type casting, wrapper classes, var, memory use
Libraries	java.lang, java.util, java.text