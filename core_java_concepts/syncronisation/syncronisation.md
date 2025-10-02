<<<<<<< HEAD
Here’s a complete guide on Java Synchronization from basic to advanced, including concepts, syntax, examples, and best practices.

Java Synchronization: Basic to Advanced
1. What is Synchronization?

Synchronization in Java is a mechanism that controls access to shared resources by multiple threads to prevent data inconsistency or race conditions.

When multiple threads access and modify shared data concurrently, the results can be unpredictable. Synchronization ensures that only one thread at a time can access the critical section of code.

2. Why is Synchronization Needed?

Consider this example without synchronization:

class Counter {
    int count = 0;
    void increment() {
        count++;  // Not atomic, can cause race condition
    }
}


If two threads call increment() simultaneously, the final count might be wrong because increment involves multiple steps (read, increment, write).

3. Basic Synchronization: synchronized Keyword
a) Synchronized Method

Lock is acquired on the instance (object) for non-static methods.

class Counter {
    private int count = 0;

    public synchronized void increment() {
        count++;
    }

    public int getCount() {
        return count;
    }
}


Usage:

Counter counter = new Counter();
counter.increment(); // Thread-safe increment

b) Synchronized Block

You can synchronize only a critical section rather than the whole method for better performance.

public void increment() {
    synchronized(this) {
        count++;
    }
}


Or synchronize on any other object as a lock:

private final Object lock = new Object();

public void increment() {
    synchronized(lock) {
        count++;
    }
}

4. Synchronization on Static Methods and Blocks

Static synchronized methods lock on the Class object (ClassName.class).

public static synchronized void staticMethod() {
    // Only one thread can access this at a time per class
}


Static synchronized block example:

synchronized(ClassName.class) {
    // critical code
}

5. Intrinsic Locks / Monitor Locks

Every Java object has an intrinsic lock (monitor).

When a thread enters a synchronized block or method, it acquires the lock.

Other threads trying to enter synchronized code on the same lock will block until the lock is released.

6. Reentrant Locks

Locks are reentrant, meaning a thread holding a lock can reacquire it without deadlock.

public synchronized void method1() {
    method2();
}

public synchronized void method2() {
    // This works fine since same thread can reenter lock
}

7. Advanced Synchronization: java.util.concurrent.locks.Lock

Introduced in Java 5, provides more flexible locking:

import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

class Counter {
    private int count = 0;
    private Lock lock = new ReentrantLock();

    public void increment() {
        lock.lock();
        try {
            count++;
        } finally {
            lock.unlock();  // Always unlock in finally block
        }
    }
}


Advantages over synchronized:

Ability to try to acquire lock without waiting (tryLock())

Ability to acquire interruptibly (lockInterruptibly())

Multiple conditions support

8. Deadlock and How to Avoid It

Deadlock occurs when two or more threads wait for each other to release locks indefinitely.

Example:

class DeadlockExample {
    private final Object lock1 = new Object();
    private final Object lock2 = new Object();

    public void method1() {
        synchronized(lock1) {
            synchronized(lock2) {
                System.out.println("Inside method1");
            }
        }
    }

    public void method2() {
        synchronized(lock2) {
            synchronized(lock1) {
                System.out.println("Inside method2");
            }
        }
    }
}


Thread 1 locks lock1 and waits for lock2

Thread 2 locks lock2 and waits for lock1

Both wait forever → deadlock

Avoid deadlock by:

Lock ordering (always acquire locks in the same order)

Using tryLock with timeout

Minimize lock scope

9. Synchronization Best Practices

Synchronize only the critical section to improve performance.

Use private lock objects instead of this to avoid accidental external locking.

Always release locks in finally blocks.

Prefer higher-level concurrency utilities (Lock, Semaphore) for complex scenarios.

Avoid blocking operations inside synchronized code.

10. Example: Synchronized Counter
class Counter {
    private int count = 0;

    // Synchronized method
    public synchronized void increment() {
        count++;
    }

    public synchronized int getCount() {
        return count;
    }
}

11. Example: Using ReentrantLock
import java.util.concurrent.locks.ReentrantLock;

class Counter {
    private int count = 0;
    private ReentrantLock lock = new ReentrantLock();

    public void increment() {
        lock.lock();
        try {
            count++;
        } finally {
            lock.unlock();
        }
    }

    public int getCount() {
        return count;
    }
}

12. Example: Preventing Deadlock Using Lock Ordering
class SafeResource {
    private final Object lock1 = new Object();
    private final Object lock2 = new Object();

    public void safeMethod1() {
        synchronized(lock1) {
            synchronized(lock2) {
                System.out.println("Executing safeMethod1");
            }
        }
    }

    public void safeMethod2() {
        synchronized(lock1) {  // Lock1 first to avoid deadlock
            synchronized(lock2) {
                System.out.println("Executing safeMethod2");
            }
        }
    }
}

13. Summary Table
Synchronization Type	Lock Object	Usage	Notes
Synchronized method	this (instance) or Class object (static)	Lock entire method	Simple to use
Synchronized block	Any object	Lock only critical section	More performant and flexible
ReentrantLock	Explicit lock object	Fine-grained control over locks	Supports tryLock, interruptible
wait()/notify()	Called inside synchronized block	Inter-thread communication	Requires lock on object
14. Quick Demo Program: Synchronization Example
public class SynchronizationDemo {

    static class Counter {
        private int count = 0;

        public synchronized void increment() {
            count++;
        }

        public synchronized int getCount() {
            return count;
        }
    }

    public static void main(String[] args) throws InterruptedException {
        Counter counter = new Counter();

        Runnable task = () -> {
            for (int i = 0; i < 1000; i++) {
                counter.increment();
            }
        };

        Thread t1 = new Thread(task);
        Thread t2 = new Thread(task);

        t1.start();
        t2.start();

        t1.join();
        t2.join();

        System.out.println("Final count: " + counter.getCount()); // Should be 2000
    }
}
=======
Here’s a complete guide on Java Synchronization from basic to advanced, including concepts, syntax, examples, and best practices.

Java Synchronization: Basic to Advanced
1. What is Synchronization?

Synchronization in Java is a mechanism that controls access to shared resources by multiple threads to prevent data inconsistency or race conditions.

When multiple threads access and modify shared data concurrently, the results can be unpredictable. Synchronization ensures that only one thread at a time can access the critical section of code.

2. Why is Synchronization Needed?

Consider this example without synchronization:

class Counter {
    int count = 0;
    void increment() {
        count++;  // Not atomic, can cause race condition
    }
}


If two threads call increment() simultaneously, the final count might be wrong because increment involves multiple steps (read, increment, write).

3. Basic Synchronization: synchronized Keyword
a) Synchronized Method

Lock is acquired on the instance (object) for non-static methods.

class Counter {
    private int count = 0;

    public synchronized void increment() {
        count++;
    }

    public int getCount() {
        return count;
    }
}


Usage:

Counter counter = new Counter();
counter.increment(); // Thread-safe increment

b) Synchronized Block

You can synchronize only a critical section rather than the whole method for better performance.

public void increment() {
    synchronized(this) {
        count++;
    }
}


Or synchronize on any other object as a lock:

private final Object lock = new Object();

public void increment() {
    synchronized(lock) {
        count++;
    }
}

4. Synchronization on Static Methods and Blocks

Static synchronized methods lock on the Class object (ClassName.class).

public static synchronized void staticMethod() {
    // Only one thread can access this at a time per class
}


Static synchronized block example:

synchronized(ClassName.class) {
    // critical code
}

5. Intrinsic Locks / Monitor Locks

Every Java object has an intrinsic lock (monitor).

When a thread enters a synchronized block or method, it acquires the lock.

Other threads trying to enter synchronized code on the same lock will block until the lock is released.

6. Reentrant Locks

Locks are reentrant, meaning a thread holding a lock can reacquire it without deadlock.

public synchronized void method1() {
    method2();
}

public synchronized void method2() {
    // This works fine since same thread can reenter lock
}

7. Advanced Synchronization: java.util.concurrent.locks.Lock

Introduced in Java 5, provides more flexible locking:

import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

class Counter {
    private int count = 0;
    private Lock lock = new ReentrantLock();

    public void increment() {
        lock.lock();
        try {
            count++;
        } finally {
            lock.unlock();  // Always unlock in finally block
        }
    }
}


Advantages over synchronized:

Ability to try to acquire lock without waiting (tryLock())

Ability to acquire interruptibly (lockInterruptibly())

Multiple conditions support

8. Deadlock and How to Avoid It

Deadlock occurs when two or more threads wait for each other to release locks indefinitely.

Example:

class DeadlockExample {
    private final Object lock1 = new Object();
    private final Object lock2 = new Object();

    public void method1() {
        synchronized(lock1) {
            synchronized(lock2) {
                System.out.println("Inside method1");
            }
        }
    }

    public void method2() {
        synchronized(lock2) {
            synchronized(lock1) {
                System.out.println("Inside method2");
            }
        }
    }
}


Thread 1 locks lock1 and waits for lock2

Thread 2 locks lock2 and waits for lock1

Both wait forever → deadlock

Avoid deadlock by:

Lock ordering (always acquire locks in the same order)

Using tryLock with timeout

Minimize lock scope

9. Synchronization Best Practices

Synchronize only the critical section to improve performance.

Use private lock objects instead of this to avoid accidental external locking.

Always release locks in finally blocks.

Prefer higher-level concurrency utilities (Lock, Semaphore) for complex scenarios.

Avoid blocking operations inside synchronized code.

10. Example: Synchronized Counter
class Counter {
    private int count = 0;

    // Synchronized method
    public synchronized void increment() {
        count++;
    }

    public synchronized int getCount() {
        return count;
    }
}

11. Example: Using ReentrantLock
import java.util.concurrent.locks.ReentrantLock;

class Counter {
    private int count = 0;
    private ReentrantLock lock = new ReentrantLock();

    public void increment() {
        lock.lock();
        try {
            count++;
        } finally {
            lock.unlock();
        }
    }

    public int getCount() {
        return count;
    }
}

12. Example: Preventing Deadlock Using Lock Ordering
class SafeResource {
    private final Object lock1 = new Object();
    private final Object lock2 = new Object();

    public void safeMethod1() {
        synchronized(lock1) {
            synchronized(lock2) {
                System.out.println("Executing safeMethod1");
            }
        }
    }

    public void safeMethod2() {
        synchronized(lock1) {  // Lock1 first to avoid deadlock
            synchronized(lock2) {
                System.out.println("Executing safeMethod2");
            }
        }
    }
}

13. Summary Table
Synchronization Type	Lock Object	Usage	Notes
Synchronized method	this (instance) or Class object (static)	Lock entire method	Simple to use
Synchronized block	Any object	Lock only critical section	More performant and flexible
ReentrantLock	Explicit lock object	Fine-grained control over locks	Supports tryLock, interruptible
wait()/notify()	Called inside synchronized block	Inter-thread communication	Requires lock on object
14. Quick Demo Program: Synchronization Example
public class SynchronizationDemo {

    static class Counter {
        private int count = 0;

        public synchronized void increment() {
            count++;
        }

        public synchronized int getCount() {
            return count;
        }
    }

    public static void main(String[] args) throws InterruptedException {
        Counter counter = new Counter();

        Runnable task = () -> {
            for (int i = 0; i < 1000; i++) {
                counter.increment();
            }
        };

        Thread t1 = new Thread(task);
        Thread t2 = new Thread(task);

        t1.start();
        t2.start();

        t1.join();
        t2.join();

        System.out.println("Final count: " + counter.getCount()); // Should be 2000
    }
}
>>>>>>> 3b36c0597166863e15545dafb8ceb347a40d878a
