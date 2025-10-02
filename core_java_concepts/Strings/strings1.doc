<<<<<<< HEAD
Let’s dive into the String topic in Java, starting from the basics to more advanced concepts, including predefined methods and the sub-packages associated with it.

1. Introduction to Strings

In Java, strings are objects that represent sequences of characters. Unlike primitive types, strings are immutable, meaning once created, their content cannot be changed.

Example: Basic String Usage
public class BasicString {
    public static void main(String[] args) {
        String greeting = "Hello, World!"; // String initialization
        System.out.println(greeting); // Output the string
    }
}


Explanation:

A string is declared and initialized using double quotes (" ").

The String class in Java is part of the java.lang package, so you don't need to import it.

2. String Methods (Predefined)

Java's String class provides a wide variety of methods to perform common operations on strings.

2.1 Length of a String
public class StringLength {
    public static void main(String[] args) {
        String name = "Java Programming";
        int length = name.length(); // Returns the length of the string
        System.out.println("Length: " + length); // Output: 16
    }
}

2.2 Substring

You can extract a portion of a string using the substring() method.

public class StringSubstring {
    public static void main(String[] args) {
        String sentence = "Hello, Java!";
        String part = sentence.substring(7, 11); // Extracts "Java"
        System.out.println("Substring: " + part); // Output: Java
    }
}


Explanation:

substring(startIndex, endIndex) extracts a part of the string starting from startIndex to endIndex-1.

2.3 Convert to Uppercase/Lowercase
public class StringCase {
    public static void main(String[] args) {
        String text = "Java Programming";
        System.out.println(text.toUpperCase()); // Output: JAVA PROGRAMMING
        System.out.println(text.toLowerCase()); // Output: java programming
    }
}

2.4 Trimming Whitespace
public class StringTrim {
    public static void main(String[] args) {
        String text = "   Hello Java   ";
        System.out.println(text.trim()); // Output: "Hello Java" (without leading/trailing spaces)
    }
}

2.5 String Comparison
public class StringComparison {
    public static void main(String[] args) {
        String str1 = "Hello";
        String str2 = "hello";

        System.out.println(str1.equals(str2));       // false (case-sensitive)
        System.out.println(str1.equalsIgnoreCase(str2)); // true (ignores case)
    }
}


Explanation:

equals() compares two strings for equality.

equalsIgnoreCase() compares two strings ignoring case.

2.6 Replacing Characters or Substrings
public class StringReplace {
    public static void main(String[] args) {
        String sentence = "Java is awesome!";
        String newSentence = sentence.replace("awesome", "fantastic");
        System.out.println(newSentence); // Output: Java is fantastic!
    }
}

2.7 Checking String Contains/Substrings
public class StringContains {
    public static void main(String[] args) {
        String sentence = "Java programming is fun!";
        boolean contains = sentence.contains("programming");
        System.out.println("Contains 'programming': " + contains); // true
    }
}

2.8 Index of a Substring
public class StringIndex {
    public static void main(String[] args) {
        String sentence = "Hello, World!";
        int index = sentence.indexOf("World"); // Returns the starting index of the substring
        System.out.println("Index of 'World': " + index); // Output: 7
    }
}

2.9 Split String into Array
public class StringSplit {
    public static void main(String[] args) {
        String sentence = "apple,orange,banana";
        String[] fruits = sentence.split(",");  // Splitting string by comma
        for (String fruit : fruits) {
            System.out.println(fruit);
        }
    }
}

3. StringBuffer and StringBuilder

Java provides StringBuffer and StringBuilder for mutable strings. These classes are used when you need to modify a string frequently, as they are more efficient than using the String class.

3.1 StringBuffer
public class StringBufferExample {
    public static void main(String[] args) {
        StringBuffer sb = new StringBuffer("Hello");
        sb.append(" Java"); // Adds " Java" to the string
        System.out.println(sb); // Output: Hello Java
    }
}


Explanation:

StringBuffer is thread-safe, meaning it can be safely used in multi-threaded environments.

3.2 StringBuilder
public class StringBuilderExample {
    public static void main(String[] args) {
        StringBuilder sb = new StringBuilder("Hello");
        sb.append(" World");
        System.out.println(sb); // Output: Hello World
    }
}


Explanation:

StringBuilder is similar to StringBuffer but is not thread-safe and hence more efficient for single-threaded environments.

4. Advanced String Operations
4.1 Regular Expressions with Strings

Java provides support for regular expressions (regex) through the String.matches() method.

public class StringRegex {
    public static void main(String[] args) {
        String email = "test@example.com";
        boolean isValid = email.matches("[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\\.[a-zA-Z]{2,}");
        System.out.println("Is valid email: " + isValid); // Output: true
    }
}

4.2 String.format() for Formatting Strings
public class StringFormat {
    public static void main(String[] args) {
        String name = "Java";
        int year = 2025;
        String formattedString = String.format("Welcome to %s, the year is %d.", name, year);
        System.out.println(formattedString); // Output: Welcome to Java, the year is 2025.
    }
}

5. Sub-Packages of the String Class

Java provides sub-packages that extend the functionality of String. While the String class itself is part of the java.lang package, we also have some sub-packages and utility classes:

5.1 java.util.regex

The java.util.regex package contains classes for pattern matching using regular expressions.

Pattern: A compiled regular expression.

Matcher: An engine that performs matching operations on text using patterns.

Example of Pattern and Matcher:

import java.util.regex.*;

public class RegexExample {
    public static void main(String[] args) {
        Pattern pattern = Pattern.compile("a*b");
        Matcher matcher = pattern.matcher("aaab");
        System.out.println(matcher.matches()); // Output: true
    }
}

5.2 java.text

The java.text package is useful for formatting and parsing strings, particularly when working with dates, numbers, and internationalization.

MessageFormat: For creating messages that are dynamically formatted.

DateFormat: For formatting dates and times as strings.

import java.text.SimpleDateFormat;
import java.util.Date;

public class DateFormatting {
    public static void main(String[] args) {
        Date date = new Date();
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");
        System.out.println(sdf.format(date));  // Output: current date in yyyy-MM-dd format
    }
}

6. Conclusion

We've covered:

Basic operations on strings like concatenation, comparison, and substring extraction.

Advanced string handling using classes like StringBuffer and StringBuilder.

String formatting and regular expressions.

Sub-packages like java.util.regex and java.text for advanced string manipulation.

String handling is a fundamental skill in Java, and knowing how to efficiently manipulate and format strings will help in many real-world applications.
=======
Let’s dive into the String topic in Java, starting from the basics to more advanced concepts, including predefined methods and the sub-packages associated with it.

1. Introduction to Strings

In Java, strings are objects that represent sequences of characters. Unlike primitive types, strings are immutable, meaning once created, their content cannot be changed.

Example: Basic String Usage
public class BasicString {
    public static void main(String[] args) {
        String greeting = "Hello, World!"; // String initialization
        System.out.println(greeting); // Output the string
    }
}


Explanation:

A string is declared and initialized using double quotes (" ").

The String class in Java is part of the java.lang package, so you don't need to import it.

2. String Methods (Predefined)

Java's String class provides a wide variety of methods to perform common operations on strings.

2.1 Length of a String
public class StringLength {
    public static void main(String[] args) {
        String name = "Java Programming";
        int length = name.length(); // Returns the length of the string
        System.out.println("Length: " + length); // Output: 16
    }
}

2.2 Substring

You can extract a portion of a string using the substring() method.

public class StringSubstring {
    public static void main(String[] args) {
        String sentence = "Hello, Java!";
        String part = sentence.substring(7, 11); // Extracts "Java"
        System.out.println("Substring: " + part); // Output: Java
    }
}


Explanation:

substring(startIndex, endIndex) extracts a part of the string starting from startIndex to endIndex-1.

2.3 Convert to Uppercase/Lowercase
public class StringCase {
    public static void main(String[] args) {
        String text = "Java Programming";
        System.out.println(text.toUpperCase()); // Output: JAVA PROGRAMMING
        System.out.println(text.toLowerCase()); // Output: java programming
    }
}

2.4 Trimming Whitespace
public class StringTrim {
    public static void main(String[] args) {
        String text = "   Hello Java   ";
        System.out.println(text.trim()); // Output: "Hello Java" (without leading/trailing spaces)
    }
}

2.5 String Comparison
public class StringComparison {
    public static void main(String[] args) {
        String str1 = "Hello";
        String str2 = "hello";

        System.out.println(str1.equals(str2));       // false (case-sensitive)
        System.out.println(str1.equalsIgnoreCase(str2)); // true (ignores case)
    }
}


Explanation:

equals() compares two strings for equality.

equalsIgnoreCase() compares two strings ignoring case.

2.6 Replacing Characters or Substrings
public class StringReplace {
    public static void main(String[] args) {
        String sentence = "Java is awesome!";
        String newSentence = sentence.replace("awesome", "fantastic");
        System.out.println(newSentence); // Output: Java is fantastic!
    }
}

2.7 Checking String Contains/Substrings
public class StringContains {
    public static void main(String[] args) {
        String sentence = "Java programming is fun!";
        boolean contains = sentence.contains("programming");
        System.out.println("Contains 'programming': " + contains); // true
    }
}

2.8 Index of a Substring
public class StringIndex {
    public static void main(String[] args) {
        String sentence = "Hello, World!";
        int index = sentence.indexOf("World"); // Returns the starting index of the substring
        System.out.println("Index of 'World': " + index); // Output: 7
    }
}

2.9 Split String into Array
public class StringSplit {
    public static void main(String[] args) {
        String sentence = "apple,orange,banana";
        String[] fruits = sentence.split(",");  // Splitting string by comma
        for (String fruit : fruits) {
            System.out.println(fruit);
        }
    }
}

3. StringBuffer and StringBuilder

Java provides StringBuffer and StringBuilder for mutable strings. These classes are used when you need to modify a string frequently, as they are more efficient than using the String class.

3.1 StringBuffer
public class StringBufferExample {
    public static void main(String[] args) {
        StringBuffer sb = new StringBuffer("Hello");
        sb.append(" Java"); // Adds " Java" to the string
        System.out.println(sb); // Output: Hello Java
    }
}


Explanation:

StringBuffer is thread-safe, meaning it can be safely used in multi-threaded environments.

3.2 StringBuilder
public class StringBuilderExample {
    public static void main(String[] args) {
        StringBuilder sb = new StringBuilder("Hello");
        sb.append(" World");
        System.out.println(sb); // Output: Hello World
    }
}


Explanation:

StringBuilder is similar to StringBuffer but is not thread-safe and hence more efficient for single-threaded environments.

4. Advanced String Operations
4.1 Regular Expressions with Strings

Java provides support for regular expressions (regex) through the String.matches() method.

public class StringRegex {
    public static void main(String[] args) {
        String email = "test@example.com";
        boolean isValid = email.matches("[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\\.[a-zA-Z]{2,}");
        System.out.println("Is valid email: " + isValid); // Output: true
    }
}

4.2 String.format() for Formatting Strings
public class StringFormat {
    public static void main(String[] args) {
        String name = "Java";
        int year = 2025;
        String formattedString = String.format("Welcome to %s, the year is %d.", name, year);
        System.out.println(formattedString); // Output: Welcome to Java, the year is 2025.
    }
}

5. Sub-Packages of the String Class

Java provides sub-packages that extend the functionality of String. While the String class itself is part of the java.lang package, we also have some sub-packages and utility classes:

5.1 java.util.regex

The java.util.regex package contains classes for pattern matching using regular expressions.

Pattern: A compiled regular expression.

Matcher: An engine that performs matching operations on text using patterns.

Example of Pattern and Matcher:

import java.util.regex.*;

public class RegexExample {
    public static void main(String[] args) {
        Pattern pattern = Pattern.compile("a*b");
        Matcher matcher = pattern.matcher("aaab");
        System.out.println(matcher.matches()); // Output: true
    }
}

5.2 java.text

The java.text package is useful for formatting and parsing strings, particularly when working with dates, numbers, and internationalization.

MessageFormat: For creating messages that are dynamically formatted.

DateFormat: For formatting dates and times as strings.

import java.text.SimpleDateFormat;
import java.util.Date;

public class DateFormatting {
    public static void main(String[] args) {
        Date date = new Date();
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");
        System.out.println(sdf.format(date));  // Output: current date in yyyy-MM-dd format
    }
}

6. Conclusion

We've covered:

Basic operations on strings like concatenation, comparison, and substring extraction.

Advanced string handling using classes like StringBuffer and StringBuilder.

String formatting and regular expressions.

Sub-packages like java.util.regex and java.text for advanced string manipulation.

String handling is a fundamental skill in Java, and knowing how to efficiently manipulate and format strings will help in many real-world applications.
>>>>>>> 3b36c0597166863e15545dafb8ceb347a40d878a
