Here’s a complete Java Multithreading guide from basic to advanced covering concepts, syntax, examples, and real-world scenarios.

Java Multithreading: Basic to Advanced
1. What is Multithreading?

Multithreading allows concurrent execution of two or more threads (lightweight processes) for better CPU utilization and responsive programs.

2. Thread Basics

Thread: Smallest unit of execution within a process.

Process: Program in execution.

Main Thread: Default thread that runs your main() method.

3. Ways to Create Threads
a) Extending Thread class
class MyThread extends Thread {
    public void run() {
        System.out.println("Thread running: " + Thread.currentThread().getName());
    }
}

public class Test {
    public static void main(String[] args) {
        MyThread t1 = new MyThread();
        t1.start();  // Starts a new thread and calls run()
    }
}

b) Implementing Runnable interface
class MyRunnable implements Runnable {
    public void run() {
        System.out.println("Thread running: " + Thread.currentThread().getName());
    }
}

public class Test {
    public static void main(String[] args) {
        Thread t1 = new Thread(new MyRunnable());
        t1.start();
    }
}

4. Thread Lifecycle
State	Description
New	Thread created but not started
Runnable	Ready to run, waiting for CPU time
Running	Thread executing
Blocked/Waiting	Waiting for resource or event
Terminated	Execution finished or stopped
5. Thread Methods
Method	Description
start()	Begins thread execution
run()	Code executed by thread
sleep(ms)	Pause thread for given milliseconds
join()	Wait for another thread to finish
yield()	Pause and allow other threads to run
interrupt()	Interrupt thread’s execution
setPriority()	Set thread priority (1 to 10)
6. Synchronization

When multiple threads access shared resources, synchronization avoids race conditions.

class Counter {
    private int count = 0;

    public synchronized void increment() {
        count++;
    }

    public int getCount() {
        return count;
    }
}

7. Inter-thread Communication: wait(), notify(), notifyAll()

Used to coordinate threads.

class Data {
    private int number;
    private boolean available = false;

    public synchronized void produce(int num) throws InterruptedException {
        while (available) wait();
        number = num;
        available = true;
        notify();
    }

    public synchronized int consume() throws InterruptedException {
        while (!available) wait();
        available = false;
        notify();
        return number;
    }
}

8. Thread-safe Collections and Utilities (Java 5+)

ConcurrentHashMap

CopyOnWriteArrayList

BlockingQueue

Semaphore, CountDownLatch, CyclicBarrier

9. Thread Pools (Executor Framework)
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

ExecutorService executor = Executors.newFixedThreadPool(3);

for (int i = 0; i < 5; i++) {
    int finalI = i;
    executor.execute(() -> {
        System.out.println("Running task " + finalI + " by " + Thread.currentThread().getName());
    });
}

executor.shutdown();

10. Advanced Topics
a) Volatile Keyword

Ensures visibility of changes to variables across threads.

volatile boolean flag = true;

b) Deadlock

Occurs when two or more threads wait indefinitely for resources locked by each other.

c) Livelock & Starvation

Livelock: Threads keep changing state in response to others but can’t proceed.

Starvation: Threads never get CPU time due to thread priorities.

d) Callable and Future (Java 5+)

Supports threads returning values.

import java.util.concurrent.*;

Callable<Integer> task = () -> {
    Thread.sleep(1000);
    return 123;
};

ExecutorService executor = Executors.newSingleThreadExecutor();
Future<Integer> future = executor.submit(task);

System.out.println("Result: " + future.get());
executor.shutdown();

11. Example: Producer-Consumer with Wait/Notify
class ProducerConsumer {
    private final List<Integer> buffer = new LinkedList<>();
    private final int MAX_SIZE = 5;

    public void produce() throws InterruptedException {
        int value = 0;
        synchronized (this) {
            while (buffer.size() == MAX_SIZE) wait();

            buffer.add(value++);
            System.out.println("Produced: " + value);
            notify();

        }
    }

    public void consume() throws InterruptedException {
        synchronized (this) {
            while (buffer.isEmpty()) wait();

            int val = buffer.remove(0);
            System.out.println("Consumed: " + val);
            notify();
        }
    }
}

12. Complete Runnable Example: Multithreading Demo
public class MultithreadDemo implements Runnable {
    private String threadName;

    MultithreadDemo(String name) {
        this.threadName = name;
    }

    public void run() {
        try {
            for (int i=0; i<5; i++) {
                System.out.println(threadName + " is running: " + i);
                Thread.sleep(500);
            }
        } catch (InterruptedException e) {
            System.out.println(threadName + " interrupted.");
        }
    }

    public static void main(String[] args) {
        Thread t1 = new Thread(new MultithreadDemo("Thread-1"));
        Thread t2 = new Thread(new MultithreadDemo("Thread-2"));

        t1.start();
        t2.start();
    }
}

Summary
Topic	Description
Thread Creation	Extend Thread or implement Runnable
Synchronization	synchronized keyword, locks
Communication	wait(), notify(), notifyAll()
Concurrency Utils	ExecutorService, Locks, Concurrent collections
Advanced	Deadlock, Volatile, Callable/Future

If you want, I can prepare a ready-to-run file with comments or dive into any specific part — like deadlocks, thread pools, or concurrency utilities. Just ask!

You said:
yes
ChatGPT said:

Great! Here’s a ready-to-run Java program covering multithreading basics to some advanced concepts with detailed comments to help you understand step-by-step.

import java.util.concurrent.*;

// Demo class implementing Runnable to create threads
class MultithreadDemo implements Runnable {
    private String threadName;

    MultithreadDemo(String name) {
        this.threadName = name;
    }

    // Code executed by thread
    public void run() {
        try {
            for (int i = 0; i < 5; i++) {
                System.out.println(threadName + " running iteration " + i);
                Thread.sleep(500); // Simulate work
            }
        } catch (InterruptedException e) {
            System.out.println(threadName + " interrupted.");
        }
        System.out.println(threadName + " finished execution.");
    }
}

// Shared resource class with synchronized methods (thread-safe)
class Counter {
    private int count = 0;

    // synchronized to avoid race conditions
    public synchronized void increment() {
        count++;
    }

    public int getCount() {
        return count;
    }
}

// Producer-Consumer example using wait() and notify()
class ProducerConsumer {
    private final LinkedList<Integer> buffer = new LinkedList<>();
    private final int MAX_SIZE = 5;

    // Produce numbers and add to buffer
    public void produce() throws InterruptedException {
        int value = 0;
        while (true) {
            synchronized (this) {
                // Wait if buffer full
                while (buffer.size() == MAX_SIZE) {
                    wait();
                }
                buffer.add(value);
                System.out.println("Produced: " + value);
                value++;
                notify(); // Notify consumer
            }
            Thread.sleep(300);
        }
    }

    // Consume numbers from buffer
    public void consume() throws InterruptedException {
        while (true) {
            synchronized (this) {
                // Wait if buffer empty
                while (buffer.isEmpty()) {
                    wait();
                }
                int val = buffer.removeFirst();
                System.out.println("Consumed: " + val);
                notify(); // Notify producer
            }
            Thread.sleep(500);
        }
    }
}

public class MultithreadingFullDemo {

    public static void main(String[] args) throws InterruptedException, ExecutionException {
        System.out.println("=== Basic Thread Creation and Execution ===");
        Thread t1 = new Thread(new MultithreadDemo("Thread-1"));
        Thread t2 = new Thread(new MultithreadDemo("Thread-2"));
        t1.start();
        t2.start();

        t1.join(); // Wait for t1 to finish
        t2.join(); // Wait for t2 to finish

        System.out.println("\n=== Synchronization Demo ===");
        Counter counter = new Counter();

        Runnable task = () -> {
            for (int i = 0; i < 1000; i++) {
                counter.increment();
            }
        };

        Thread th1 = new Thread(task);
        Thread th2 = new Thread(task);
        th1.start();
        th2.start();

        th1.join();
        th2.join();

        System.out.println("Counter value (should be 2000): " + counter.getCount());

        System.out.println("\n=== Producer-Consumer Demo ===");
        ProducerConsumer pc = new ProducerConsumer();

        Thread producer = new Thread(() -> {
            try {
                pc.produce();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        });

        Thread consumer = new Thread(() -> {
            try {
                pc.consume();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        });

        producer.start();
        consumer.start();

        // Let producer-consumer run for some time then interrupt
        Thread.sleep(5000);
        producer.interrupt();
        consumer.interrupt();

        producer.join();
        consumer.join();

        System.out.println("\n=== ExecutorService and Callable Demo ===");
        ExecutorService executor = Executors.newFixedThreadPool(2);

        Callable<String> callableTask = () -> {
            Thread.sleep(1000);
            return "Callable Result";
        };

        Future<String> future = executor.submit(callableTask);

        System.out.println("Waiting for Callable to complete...");
        System.out.println("Callable returned: " + future.get());

        executor.shutdown();
    }
}

What this program covers:

Creating threads using Runnable

Starting and joining threads

Synchronization with synchronized keyword

Race condition prevention with synchronized increment

Producer-Consumer pattern with wait() and notify()

Thread interruption

Using ExecutorService and Callable to run tasks returning values

How to run:

Save as MultithreadingFullDemo.java

Compile: javac MultithreadingFullDemo.java

Run: java MultithreadingFullDemo