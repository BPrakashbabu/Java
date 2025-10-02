<<<<<<< HEAD
Here’s a complete guide to Regex (Regular Expressions) in Java from basic to advanced, with examples and practical use cases.

Regex in Java: Basic to Advanced
1. What is Regex?

Regular expressions are patterns used to match character combinations in strings.

Java uses the java.util.regex package which mainly has two classes:

Pattern — represents the regex pattern (compiled)

Matcher — engine that performs match operations on a character sequence

2. Basic Syntax & Special Characters
Symbol	Meaning	Example
.	Any character except newline	a.c matches abc
\d	Digit [0-9]	\d{3} matches 123
\D	Non-digit	\D+ matches letters
\w	Word character [a-zA-Z0-9_]	\w+ matches words
\W	Non-word character	\W+ matches spaces
\s	Whitespace	\s+ matches spaces
\S	Non-whitespace	\S+ matches words
^	Start of string	^abc matches at start
$	End of string	xyz$ matches at end
*	Zero or more	a* matches ``, a, aa
+	One or more	a+ matches a, aa
?	Zero or one (optional)	a? matches ``, a
{n}	Exactly n times	a{3} matches aaa
{n,}	n or more times	a{2,} matches aa+
{n,m}	Between n and m times	a{1,3} matches a to aaa
`	`	OR operator
()	Grouping / capturing group	(abc)+ matches abcabc
[]	Character class	[abc] matches a or b or c
\	Escape special char	\. matches dot literally
3. How to Use Regex in Java
import java.util.regex.*;

public class RegexExample {
    public static void main(String[] args) {
        String text = "Hello 1234";
        String pattern = "\\d+";

        Pattern p = Pattern.compile(pattern);   // compile regex
        Matcher m = p.matcher(text);            // create matcher

        while (m.find()) {
            System.out.println("Found: " + m.group());
        }
    }
}


Output:

Found: 1234

4. Common Regex Patterns
Pattern	Matches
\d+	One or more digits
\w+	One or more word chars
[a-zA-Z]+	One or more letters only
^[a-zA-Z0-9_]{3,10}$	3 to 10 alphanumeric chars (start-end)
\b\w{4}\b	Exactly 4-letter words
\s+	One or more whitespace chars
5. Grouping and Capturing
String text = "John: 1234, Alice: 5678";
Pattern p = Pattern.compile("(\\w+): (\\d+)");
Matcher m = p.matcher(text);

while (m.find()) {
    System.out.println("Name: " + m.group(1));
    System.out.println("Number: " + m.group(2));
}


Output:

Name: John
Number: 1234
Name: Alice
Number: 5678

6. Advanced Regex Features
a) Lookahead and Lookbehind (Zero-width assertions)

Positive lookahead: X(?=Y) — match X if followed by Y

Negative lookahead: X(?!Y) — match X if NOT followed by Y

Positive lookbehind: (?<=Y)X — match X if preceded by Y

Negative lookbehind: (?<!Y)X — match X if NOT preceded by Y

Example: Find foo followed by digits

String pattern = "foo(?=\\d+)";

b) Non-capturing groups
(?:abc)+  // match one or more "abc" but don't capture group

c) Atomic groups (prevent backtracking)
(?>abc)+

7. Useful Java Regex Methods
Method	Description
Pattern.compile(String)	Compiles regex into Pattern
Matcher.matches()	Matches entire input string
Matcher.find()	Finds next matching substring
Matcher.group()	Returns matched substring
String.replaceAll(regex, replacement)	Replace all matches
String.split(regex)	Split string by regex
8. Real-Time Examples and Common Problems
1) Validate Email Address
String email = "example@test.com";
String regex = "^[A-Za-z0-9+_.-]+@[A-Za-z0-9.-]+$";

boolean isValid = email.matches(regex);
System.out.println(isValid);  // true or false

2) Validate Phone Number (US)
String phone = "123-456-7890";
String regex = "^\\d{3}-\\d{3}-\\d{4}$";

System.out.println(phone.matches(regex));  // true

3) Extract hashtags from text
String text = "I love #Java and #regex!";
Pattern p = Pattern.compile("#(\\w+)");
Matcher m = p.matcher(text);

while (m.find()) {
    System.out.println("Hashtag: " + m.group(1));
}


Output:

Hashtag: Java
Hashtag: regex

4) Password validation (8-20 chars, at least 1 digit, 1 uppercase, 1 lowercase, 1 special char)
String password = "Abc123!@#";
String regex = "^(?=.*[0-9])(?=.*[a-z])(?=.*[A-Z])(?=.*[@#$%^&+=]).{8,20}$";

System.out.println(password.matches(regex));  // true or false

9. Performance Tips

Avoid catastrophic backtracking by keeping regex simple.

Prefer possessive quantifiers (*+, ++, ?+) where applicable.

Compile regex once if used multiple times (Pattern.compile).

Use non-capturing groups (?:...) when capture is not needed.

10. Summary Cheat Sheet
Concept	Regex Example	Java String
Any digit	\d	"\\d"
One or more digits	\d+	"\\d+"
Start of string	^	"^"
End of string	$	"$"
Zero or more	*	"*"
One or more	+	"+"
Optional	?	"?"
Character class	[a-zA-Z]	"[a-zA-Z]"
Capture group	(abc)	"(abc)"
Escape literal dot	\.	"\\."
Positive lookahead	X(?=Y)	"X(?=Y)"
Negative lookahead	X(?!Y)	"X(?!Y)"

If you want, I can prepare:

A ready-to-run Java example with various regex tasks

Regex cheat sheet printable PDF

Or dive into Java Pattern + Matcher class usage in a single file

Would you like me to do that?

You said:
yes
ChatGPT said:

Awesome! Here’s a ready-to-run Java program demonstrating regex basics to advanced concepts with explanations and examples:

import java.util.regex.*;

public class RegexDemo {

    // Helper method to test regex matches on input string
    public static void testRegex(String input, String pattern) {
        System.out.println("Input: " + input);
        System.out.println("Pattern: " + pattern);

        Pattern p = Pattern.compile(pattern);
        Matcher m = p.matcher(input);

        boolean found = false;
        while (m.find()) {
            System.out.println("Found: " + m.group());
            found = true;
        }

        if (!found) System.out.println("No match found.");
        System.out.println("-------------------------");
    }

    public static void main(String[] args) {
        // Basic digit matching
        testRegex("Order1234", "\\d+");    // match digits

        // Word characters
        testRegex("Hello_World", "\\w+");  // match word characters

        // Email validation (simple)
        String email = "user.name+100@test-email.com";
        String emailRegex = "^[A-Za-z0-9+_.-]+@[A-Za-z0-9.-]+$";
        System.out.println(email + " valid email? " + email.matches(emailRegex));
        System.out.println("-------------------------");

        // Extract hashtags from sentence
        String tweet = "Loving #Java and #Regex for #Coding!";
        testRegex(tweet, "#(\\w+)");

        // Password validation example
        String pwd = "Abc123!@#";
        String pwdRegex = "^(?=.*[0-9])(?=.*[a-z])(?=.*[A-Z])(?=.*[@#$%^&+=]).{8,20}$";
        System.out.println("Password valid? " + pwd.matches(pwdRegex));
        System.out.println("-------------------------");

        // Grouping and capturing names and numbers
        String data = "John: 1234, Alice: 5678";
        Pattern pattern = Pattern.compile("(\\w+): (\\d+)");
        Matcher matcher = pattern.matcher(data);
        while (matcher.find()) {
            System.out.println("Name: " + matcher.group(1));
            System.out.println("Number: " + matcher.group(2));
        }
        System.out.println("-------------------------");

        // Lookahead example: match 'foo' followed by digits
        testRegex("foo123 fooabc foo4567", "foo(?=\\d+)");

        // Replace all whitespace with dash
        String sentence = "This is a test.";
        System.out.println("Original: " + sentence);
        System.out.println("Replaced whitespace with dash: " + sentence.replaceAll("\\s", "-"));

        System.out.println("-------------------------");

        // Splitting strings using regex
        String csv = "apple,banana,,orange,grape";
        String[] fruits = csv.split(",");
        System.out.println("Split fruits:");
        for (String f : fruits) {
            System.out.println("'" + f + "'");
        }
    }
}

How to run:

Copy-paste this into a file named RegexDemo.java.

Compile: javac RegexDemo.java

Run: java RegexDemo

What this program covers:

Digit, word, and hashtag matching

Email validation regex

Password validation regex

Group capturing with Matcher

Lookahead assertions

String replacement using regex

Splitting strings by regex
=======
Here’s a complete guide to Regex (Regular Expressions) in Java from basic to advanced, with examples and practical use cases.

Regex in Java: Basic to Advanced
1. What is Regex?

Regular expressions are patterns used to match character combinations in strings.

Java uses the java.util.regex package which mainly has two classes:

Pattern — represents the regex pattern (compiled)

Matcher — engine that performs match operations on a character sequence

2. Basic Syntax & Special Characters
Symbol	Meaning	Example
.	Any character except newline	a.c matches abc
\d	Digit [0-9]	\d{3} matches 123
\D	Non-digit	\D+ matches letters
\w	Word character [a-zA-Z0-9_]	\w+ matches words
\W	Non-word character	\W+ matches spaces
\s	Whitespace	\s+ matches spaces
\S	Non-whitespace	\S+ matches words
^	Start of string	^abc matches at start
$	End of string	xyz$ matches at end
*	Zero or more	a* matches ``, a, aa
+	One or more	a+ matches a, aa
?	Zero or one (optional)	a? matches ``, a
{n}	Exactly n times	a{3} matches aaa
{n,}	n or more times	a{2,} matches aa+
{n,m}	Between n and m times	a{1,3} matches a to aaa
`	`	OR operator
()	Grouping / capturing group	(abc)+ matches abcabc
[]	Character class	[abc] matches a or b or c
\	Escape special char	\. matches dot literally
3. How to Use Regex in Java
import java.util.regex.*;

public class RegexExample {
    public static void main(String[] args) {
        String text = "Hello 1234";
        String pattern = "\\d+";

        Pattern p = Pattern.compile(pattern);   // compile regex
        Matcher m = p.matcher(text);            // create matcher

        while (m.find()) {
            System.out.println("Found: " + m.group());
        }
    }
}


Output:

Found: 1234

4. Common Regex Patterns
Pattern	Matches
\d+	One or more digits
\w+	One or more word chars
[a-zA-Z]+	One or more letters only
^[a-zA-Z0-9_]{3,10}$	3 to 10 alphanumeric chars (start-end)
\b\w{4}\b	Exactly 4-letter words
\s+	One or more whitespace chars
5. Grouping and Capturing
String text = "John: 1234, Alice: 5678";
Pattern p = Pattern.compile("(\\w+): (\\d+)");
Matcher m = p.matcher(text);

while (m.find()) {
    System.out.println("Name: " + m.group(1));
    System.out.println("Number: " + m.group(2));
}


Output:

Name: John
Number: 1234
Name: Alice
Number: 5678

6. Advanced Regex Features
a) Lookahead and Lookbehind (Zero-width assertions)

Positive lookahead: X(?=Y) — match X if followed by Y

Negative lookahead: X(?!Y) — match X if NOT followed by Y

Positive lookbehind: (?<=Y)X — match X if preceded by Y

Negative lookbehind: (?<!Y)X — match X if NOT preceded by Y

Example: Find foo followed by digits

String pattern = "foo(?=\\d+)";

b) Non-capturing groups
(?:abc)+  // match one or more "abc" but don't capture group

c) Atomic groups (prevent backtracking)
(?>abc)+

7. Useful Java Regex Methods
Method	Description
Pattern.compile(String)	Compiles regex into Pattern
Matcher.matches()	Matches entire input string
Matcher.find()	Finds next matching substring
Matcher.group()	Returns matched substring
String.replaceAll(regex, replacement)	Replace all matches
String.split(regex)	Split string by regex
8. Real-Time Examples and Common Problems
1) Validate Email Address
String email = "example@test.com";
String regex = "^[A-Za-z0-9+_.-]+@[A-Za-z0-9.-]+$";

boolean isValid = email.matches(regex);
System.out.println(isValid);  // true or false

2) Validate Phone Number (US)
String phone = "123-456-7890";
String regex = "^\\d{3}-\\d{3}-\\d{4}$";

System.out.println(phone.matches(regex));  // true

3) Extract hashtags from text
String text = "I love #Java and #regex!";
Pattern p = Pattern.compile("#(\\w+)");
Matcher m = p.matcher(text);

while (m.find()) {
    System.out.println("Hashtag: " + m.group(1));
}


Output:

Hashtag: Java
Hashtag: regex

4) Password validation (8-20 chars, at least 1 digit, 1 uppercase, 1 lowercase, 1 special char)
String password = "Abc123!@#";
String regex = "^(?=.*[0-9])(?=.*[a-z])(?=.*[A-Z])(?=.*[@#$%^&+=]).{8,20}$";

System.out.println(password.matches(regex));  // true or false

9. Performance Tips

Avoid catastrophic backtracking by keeping regex simple.

Prefer possessive quantifiers (*+, ++, ?+) where applicable.

Compile regex once if used multiple times (Pattern.compile).

Use non-capturing groups (?:...) when capture is not needed.

10. Summary Cheat Sheet
Concept	Regex Example	Java String
Any digit	\d	"\\d"
One or more digits	\d+	"\\d+"
Start of string	^	"^"
End of string	$	"$"
Zero or more	*	"*"
One or more	+	"+"
Optional	?	"?"
Character class	[a-zA-Z]	"[a-zA-Z]"
Capture group	(abc)	"(abc)"
Escape literal dot	\.	"\\."
Positive lookahead	X(?=Y)	"X(?=Y)"
Negative lookahead	X(?!Y)	"X(?!Y)"

If you want, I can prepare:

A ready-to-run Java example with various regex tasks

Regex cheat sheet printable PDF

Or dive into Java Pattern + Matcher class usage in a single file

Would you like me to do that?

You said:
yes
ChatGPT said:

Awesome! Here’s a ready-to-run Java program demonstrating regex basics to advanced concepts with explanations and examples:

import java.util.regex.*;

public class RegexDemo {

    // Helper method to test regex matches on input string
    public static void testRegex(String input, String pattern) {
        System.out.println("Input: " + input);
        System.out.println("Pattern: " + pattern);

        Pattern p = Pattern.compile(pattern);
        Matcher m = p.matcher(input);

        boolean found = false;
        while (m.find()) {
            System.out.println("Found: " + m.group());
            found = true;
        }

        if (!found) System.out.println("No match found.");
        System.out.println("-------------------------");
    }

    public static void main(String[] args) {
        // Basic digit matching
        testRegex("Order1234", "\\d+");    // match digits

        // Word characters
        testRegex("Hello_World", "\\w+");  // match word characters

        // Email validation (simple)
        String email = "user.name+100@test-email.com";
        String emailRegex = "^[A-Za-z0-9+_.-]+@[A-Za-z0-9.-]+$";
        System.out.println(email + " valid email? " + email.matches(emailRegex));
        System.out.println("-------------------------");

        // Extract hashtags from sentence
        String tweet = "Loving #Java and #Regex for #Coding!";
        testRegex(tweet, "#(\\w+)");

        // Password validation example
        String pwd = "Abc123!@#";
        String pwdRegex = "^(?=.*[0-9])(?=.*[a-z])(?=.*[A-Z])(?=.*[@#$%^&+=]).{8,20}$";
        System.out.println("Password valid? " + pwd.matches(pwdRegex));
        System.out.println("-------------------------");

        // Grouping and capturing names and numbers
        String data = "John: 1234, Alice: 5678";
        Pattern pattern = Pattern.compile("(\\w+): (\\d+)");
        Matcher matcher = pattern.matcher(data);
        while (matcher.find()) {
            System.out.println("Name: " + matcher.group(1));
            System.out.println("Number: " + matcher.group(2));
        }
        System.out.println("-------------------------");

        // Lookahead example: match 'foo' followed by digits
        testRegex("foo123 fooabc foo4567", "foo(?=\\d+)");

        // Replace all whitespace with dash
        String sentence = "This is a test.";
        System.out.println("Original: " + sentence);
        System.out.println("Replaced whitespace with dash: " + sentence.replaceAll("\\s", "-"));

        System.out.println("-------------------------");

        // Splitting strings using regex
        String csv = "apple,banana,,orange,grape";
        String[] fruits = csv.split(",");
        System.out.println("Split fruits:");
        for (String f : fruits) {
            System.out.println("'" + f + "'");
        }
    }
}

How to run:

Copy-paste this into a file named RegexDemo.java.

Compile: javac RegexDemo.java

Run: java RegexDemo

What this program covers:

Digit, word, and hashtag matching

Email validation regex

Password validation regex

Group capturing with Matcher

Lookahead assertions

String replacement using regex

Splitting strings by regex
>>>>>>> 3b36c0597166863e15545dafb8ceb347a40d878a
