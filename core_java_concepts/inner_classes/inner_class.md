<<<<<<< HEAD
Here’s a comprehensive guide on Java Inner Classes from basic to advanced, including all types, syntax, use cases, and real-world examples.

Java Inner Classes: Basic to Advanced
1. What are Inner Classes?

Inner classes are classes defined within another class. They are used to logically group classes, increase encapsulation, and can access members of the outer class including private ones.

2. Types of Inner Classes in Java
Inner Class Type	Description
Member Inner Class	Non-static class defined inside another class
Static Nested Class	Static class defined inside another class
Local Inner Class	Class defined inside a method or block
Anonymous Inner Class	Class without a name, defined and instantiated in one place
3. Member Inner Class
Syntax
class Outer {
    class Inner {
        void display() {
            System.out.println("Inside member inner class");
        }
    }
}

Usage
Outer outer = new Outer();
Outer.Inner inner = outer.new Inner();
inner.display();

Notes

Has access to all members (even private) of outer class.

Cannot declare static members (except final constants).

4. Static Nested Class
Syntax
class Outer {
    static class Nested {
        void show() {
            System.out.println("Inside static nested class");
        }
    }
}

Usage
Outer.Nested nested = new Outer.Nested();
nested.show();

Notes

Cannot access non-static members of outer class.

Behaves like a top-level class but nested for packaging.

5. Local Inner Class
Syntax
class Outer {
    void method() {
        class Local {
            void print() {
                System.out.println("Inside local inner class");
            }
        }
        Local local = new Local();
        local.print();
    }
}

Notes

Defined inside a method or block.

Can access final or effectively final variables from the enclosing method.

Used for short-lived logic.

6. Anonymous Inner Class
Syntax
Runnable r = new Runnable() {
    @Override
    public void run() {
        System.out.println("Anonymous inner class");
    }
};
new Thread(r).start();

Notes

No class name.

Instantiated at the point of definition.

Often used with interfaces or abstract classes to provide implementation inline.

7. Real-World Examples & Use Cases
a) Member Inner Class accessing outer class private members
class Outer {
    private int data = 10;

    class Inner {
        void msg() {
            System.out.println("Data is " + data);
        }
    }
}

b) Static Nested Class utility example
class Outer {
    static class Calculator {
        static int add(int a, int b) {
            return a + b;
        }
    }
}


Usage:

int result = Outer.Calculator.add(5, 3);

c) Local Inner Class in a method (e.g., for sorting)
import java.util.*;

class Outer {
    void sortList() {
        class ComparatorByLength implements Comparator<String> {
            public int compare(String a, String b) {
                return a.length() - b.length();
            }
        }
        List<String> list = Arrays.asList("apple", "pear", "banana");
        Collections.sort(list, new ComparatorByLength());
        System.out.println(list);
    }
}

d) Anonymous Inner Class for Event Handling (typical GUI)
button.addActionListener(new ActionListener() {
    @Override
    public void actionPerformed(ActionEvent e) {
        System.out.println("Button clicked");
    }
});

8. Advanced Topics
a) Accessing Outer Class Members from Inner Class

Inner classes can directly access members including private of outer class.

class Outer {
    private String msg = "Hello";

    class Inner {
        void print() {
            System.out.println(msg);  // Access outer class private member
        }
    }
}

b) Shadowing in Inner Classes

If inner class declares a variable with the same name as outer class:

class Outer {
    int x = 10;
    class Inner {
        int x = 20;
        void show() {
            System.out.println(x);            // 20 (inner)
            System.out.println(Outer.this.x); // 10 (outer)
        }
    }
}

c) Inner Classes & Serialization

Inner classes have a reference to their outer class, so serializing them serializes the outer class reference as well.

d) Inner Classes in Interfaces and Enums

Inner classes can be declared in interfaces (implicitly public static).

Enums can have inner classes just like normal classes.

9. Summary Table
Inner Class Type	Declared Inside	Static Allowed?	Can access outer instance variables?	Usage Example
Member Inner Class	Class	No	Yes	Group related helper class
Static Nested Class	Class	Yes	No	Utility classes
Local Inner Class	Method/block	No	Yes (final vars only)	Method-specific logic
Anonymous Inner Class	Expression	No	Yes	Inline implementations (listeners)
10. Complete Example Program Demonstrating All Types
public class InnerClassDemo {

    private String outerMsg = "Outer Message";

    // Member Inner Class
    class MemberInner {
        void show() {
            System.out.println("Member Inner Class: " + outerMsg);
        }
    }

    // Static Nested Class
    static class StaticNested {
        void display() {
            System.out.println("Static Nested Class");
        }
    }

    void methodWithLocalClass() {
        final String localVar = "Local Var";

        // Local Inner Class
        class LocalInner {
            void print() {
                System.out.println("Local Inner Class: " + localVar);
            }
        }

        LocalInner localInner = new LocalInner();
        localInner.print();
    }

    void methodWithAnonymousClass() {
        // Anonymous Inner Class implementing Runnable
        Runnable r = new Runnable() {
            @Override
            public void run() {
                System.out.println("Anonymous Inner Class Running");
            }
        };
        new Thread(r).start();
    }

    public static void main(String[] args) throws InterruptedException {
        InnerClassDemo outer = new InnerClassDemo();

        // Member Inner Class
        MemberInner memberInner = outer.new MemberInner();
        memberInner.show();

        // Static Nested Class
        StaticNested staticNested = new StaticNested();
        staticNested.display();

        // Local Inner Class
        outer.methodWithLocalClass();

        // Anonymous Inner Class
        outer.methodWithAnonymousClass();

        // Wait a bit for thread to print message
        Thread.sleep(500);
    }
}
=======
Here’s a comprehensive guide on Java Inner Classes from basic to advanced, including all types, syntax, use cases, and real-world examples.

Java Inner Classes: Basic to Advanced
1. What are Inner Classes?

Inner classes are classes defined within another class. They are used to logically group classes, increase encapsulation, and can access members of the outer class including private ones.

2. Types of Inner Classes in Java
Inner Class Type	Description
Member Inner Class	Non-static class defined inside another class
Static Nested Class	Static class defined inside another class
Local Inner Class	Class defined inside a method or block
Anonymous Inner Class	Class without a name, defined and instantiated in one place
3. Member Inner Class
Syntax
class Outer {
    class Inner {
        void display() {
            System.out.println("Inside member inner class");
        }
    }
}

Usage
Outer outer = new Outer();
Outer.Inner inner = outer.new Inner();
inner.display();

Notes

Has access to all members (even private) of outer class.

Cannot declare static members (except final constants).

4. Static Nested Class
Syntax
class Outer {
    static class Nested {
        void show() {
            System.out.println("Inside static nested class");
        }
    }
}

Usage
Outer.Nested nested = new Outer.Nested();
nested.show();

Notes

Cannot access non-static members of outer class.

Behaves like a top-level class but nested for packaging.

5. Local Inner Class
Syntax
class Outer {
    void method() {
        class Local {
            void print() {
                System.out.println("Inside local inner class");
            }
        }
        Local local = new Local();
        local.print();
    }
}

Notes

Defined inside a method or block.

Can access final or effectively final variables from the enclosing method.

Used for short-lived logic.

6. Anonymous Inner Class
Syntax
Runnable r = new Runnable() {
    @Override
    public void run() {
        System.out.println("Anonymous inner class");
    }
};
new Thread(r).start();

Notes

No class name.

Instantiated at the point of definition.

Often used with interfaces or abstract classes to provide implementation inline.

7. Real-World Examples & Use Cases
a) Member Inner Class accessing outer class private members
class Outer {
    private int data = 10;

    class Inner {
        void msg() {
            System.out.println("Data is " + data);
        }
    }
}

b) Static Nested Class utility example
class Outer {
    static class Calculator {
        static int add(int a, int b) {
            return a + b;
        }
    }
}


Usage:

int result = Outer.Calculator.add(5, 3);

c) Local Inner Class in a method (e.g., for sorting)
import java.util.*;

class Outer {
    void sortList() {
        class ComparatorByLength implements Comparator<String> {
            public int compare(String a, String b) {
                return a.length() - b.length();
            }
        }
        List<String> list = Arrays.asList("apple", "pear", "banana");
        Collections.sort(list, new ComparatorByLength());
        System.out.println(list);
    }
}

d) Anonymous Inner Class for Event Handling (typical GUI)
button.addActionListener(new ActionListener() {
    @Override
    public void actionPerformed(ActionEvent e) {
        System.out.println("Button clicked");
    }
});

8. Advanced Topics
a) Accessing Outer Class Members from Inner Class

Inner classes can directly access members including private of outer class.

class Outer {
    private String msg = "Hello";

    class Inner {
        void print() {
            System.out.println(msg);  // Access outer class private member
        }
    }
}

b) Shadowing in Inner Classes

If inner class declares a variable with the same name as outer class:

class Outer {
    int x = 10;
    class Inner {
        int x = 20;
        void show() {
            System.out.println(x);            // 20 (inner)
            System.out.println(Outer.this.x); // 10 (outer)
        }
    }
}

c) Inner Classes & Serialization

Inner classes have a reference to their outer class, so serializing them serializes the outer class reference as well.

d) Inner Classes in Interfaces and Enums

Inner classes can be declared in interfaces (implicitly public static).

Enums can have inner classes just like normal classes.

9. Summary Table
Inner Class Type	Declared Inside	Static Allowed?	Can access outer instance variables?	Usage Example
Member Inner Class	Class	No	Yes	Group related helper class
Static Nested Class	Class	Yes	No	Utility classes
Local Inner Class	Method/block	No	Yes (final vars only)	Method-specific logic
Anonymous Inner Class	Expression	No	Yes	Inline implementations (listeners)
10. Complete Example Program Demonstrating All Types
public class InnerClassDemo {

    private String outerMsg = "Outer Message";

    // Member Inner Class
    class MemberInner {
        void show() {
            System.out.println("Member Inner Class: " + outerMsg);
        }
    }

    // Static Nested Class
    static class StaticNested {
        void display() {
            System.out.println("Static Nested Class");
        }
    }

    void methodWithLocalClass() {
        final String localVar = "Local Var";

        // Local Inner Class
        class LocalInner {
            void print() {
                System.out.println("Local Inner Class: " + localVar);
            }
        }

        LocalInner localInner = new LocalInner();
        localInner.print();
    }

    void methodWithAnonymousClass() {
        // Anonymous Inner Class implementing Runnable
        Runnable r = new Runnable() {
            @Override
            public void run() {
                System.out.println("Anonymous Inner Class Running");
            }
        };
        new Thread(r).start();
    }

    public static void main(String[] args) throws InterruptedException {
        InnerClassDemo outer = new InnerClassDemo();

        // Member Inner Class
        MemberInner memberInner = outer.new MemberInner();
        memberInner.show();

        // Static Nested Class
        StaticNested staticNested = new StaticNested();
        staticNested.display();

        // Local Inner Class
        outer.methodWithLocalClass();

        // Anonymous Inner Class
        outer.methodWithAnonymousClass();

        // Wait a bit for thread to print message
        Thread.sleep(500);
    }
}
>>>>>>> 3b36c0597166863e15545dafb8ceb347a40d878a
