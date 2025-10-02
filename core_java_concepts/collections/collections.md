Here's a complete guide to Collections in Java, covering everything from basic concepts to advanced topics, with examples, best practices, and a class-wise breakdown.

🟢 1. What is Java Collections Framework?

Java Collections Framework (JCF) is a set of interfaces, classes, and algorithms that allow you to store, manipulate, and retrieve groups of objects efficiently.

🔑 Key Interfaces:

Collection – Root interface (List, Set, Queue extend this)

List – Ordered collection with duplicates (e.g., ArrayList, LinkedList)

Set – No duplicates (e.g., HashSet, TreeSet)

Queue – FIFO (e.g., PriorityQueue, ArrayDeque)

Map – Key-value pairs (e.g., HashMap, TreeMap)

🟡 2. List Interface (Ordered, allows duplicates)
✅ ArrayList – Dynamic array, fast random access
import java.util.*;

public class ArrayListExample {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("Java");
        list.add("Python");
        list.add("Java");  // allows duplicates

        System.out.println(list);           // [Java, Python, Java]
        System.out.println(list.get(1));    // Python
    }
}

✅ LinkedList – Doubly linked list, fast insertion/deletion
List<String> linkedList = new LinkedList<>();
linkedList.add("One");
linkedList.addFirst("Zero");
linkedList.addLast("Two");
System.out.println(linkedList);  // [Zero, One, Two]

🟠 3. Set Interface (Unordered, no duplicates)
✅ HashSet – Uses HashMap internally
Set<String> set = new HashSet<>();
set.add("Apple");
set.add("Banana");
set.add("Apple");  // Duplicate ignored
System.out.println(set);  // [Apple, Banana] – order not guaranteed

✅ LinkedHashSet – Maintains insertion order
Set<String> linkedSet = new LinkedHashSet<>();
linkedSet.add("A");
linkedSet.add("B");
linkedSet.add("A");
System.out.println(linkedSet);  // [A, B]

✅ TreeSet – Sorted, uses Red-Black Tree
Set<Integer> treeSet = new TreeSet<>();
treeSet.add(3);
treeSet.add(1);
treeSet.add(2);
System.out.println(treeSet);  // [1, 2, 3]

🔵 4. Queue Interface (FIFO)
✅ PriorityQueue – Elements ordered by priority
Queue<Integer> pq = new PriorityQueue<>();
pq.add(10);
pq.add(5);
pq.add(20);
System.out.println(pq);       // Not sorted, internal min-heap
System.out.println(pq.poll()); // 5 (smallest)

✅ ArrayDeque – Double-ended queue
Deque<String> deque = new ArrayDeque<>();
deque.addFirst("Start");
deque.addLast("End");
System.out.println(deque);  // [Start, End]

🔴 5. Map Interface (Key-Value Pairs)
✅ HashMap – No ordering, allows one null key
Map<Integer, String> map = new HashMap<>();
map.put(1, "Java");
map.put(2, "Python");
map.put(1, "Kotlin");  // Replaces "Java"
System.out.println(map);  // {1=Kotlin, 2=Python}

✅ LinkedHashMap – Maintains insertion order
Map<String, Integer> lhm = new LinkedHashMap<>();
lhm.put("One", 1);
lhm.put("Two", 2);
System.out.println(lhm);  // {One=1, Two=2}

✅ TreeMap – Sorted keys
Map<String, Integer> treeMap = new TreeMap<>();
treeMap.put("C", 3);
treeMap.put("A", 1);
treeMap.put("B", 2);
System.out.println(treeMap);  // {A=1, B=2, C=3}

🧠 6. Advanced Topics in Collections
✅ Iteration Techniques
Using Iterator
List<String> list = Arrays.asList("A", "B", "C");
Iterator<String> it = list.iterator();
while (it.hasNext()) {
    System.out.println(it.next());
}

Using forEach with Lambda
list.forEach(item -> System.out.println(item));

✅ Sorting with Collections.sort() or List.sort()
List<String> names = Arrays.asList("John", "Alice", "Bob");
Collections.sort(names);
System.out.println(names);  // [Alice, Bob, John]

✅ Custom Sorting with Comparator
List<String> names = Arrays.asList("John", "Alice", "Bob");

names.sort((a, b) -> b.compareTo(a));  // Descending
System.out.println(names);  // [John, Bob, Alice]

✅ Synchronized Collections
List<String> syncList = Collections.synchronizedList(new ArrayList<>());
Map<String, Integer> syncMap = Collections.synchronizedMap(new HashMap<>());

✅ Immutable Collections (Java 9+)
List<String> immutableList = List.of("A", "B", "C");
Set<String> immutableSet = Set.of("X", "Y", "Z");

✅ Stream API with Collections (Java 8+)
List<Integer> nums = Arrays.asList(1, 2, 3, 4, 5);
List<Integer> even = nums.stream()
                         .filter(n -> n % 2 == 0)
                         .collect(Collectors.toList());
System.out.println(even);  // [2, 4]

✅ Concurrent Collections (Java Concurrency)

ConcurrentHashMap

CopyOnWriteArrayList

BlockingQueue

Map<String, String> concurrentMap = new ConcurrentHashMap<>();
concurrentMap.put("one", "1");
System.out.println(concurrentMap.get("one"));

📚 Summary Table of Java Collections
Type	Interface	Class	  Ordered	     AllowsDuplicates	  Thread-Safe
List	List	  ArrayList	    Yes	               Yes	             No
		          LinkedList    Yes	               Yes               No
Set	      Set	    HashSet     No                 No                No
		        LinkedHashSet	 Yes               No	             No
		            TreeSet	     Sorted	           No                No
Queue	Queue	 PriorityQueue	 Partial	       Yes               No
	    Deque	   ArrayDeque	  Yes              Yes               No
Map	     Map	     HashMap	  No	         Unique keys       	 No
		          LinkedHashMap	  Yes	         Unique keys      	 No
		             TreeMap	  Sorted	     Unique keys       	 No