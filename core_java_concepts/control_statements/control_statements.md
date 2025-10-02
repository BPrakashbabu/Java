<<<<<<< HEAD
here’s a complete, practical guide to Java control statements from basic → advanced, with real-time / interview-style problems (LeetCode/HackerRank style), explanations, and ready-to-run Java code. I’ll show patterns, pitfalls, and complexity notes so you can use these constructs in real problems.

1) Quick overview — what are control statements?

Control statements let you choose execution paths and repeat actions:

Decision: if, if-else, if-else if-..., ternary ?:, switch (classic + modern switch expressions)

Loops: for, enhanced for (for-each), while, do-while

Loop control: break, continue, labeled break/continue, return

Short-circuit & boolean control: &&, || (order matters)

Other patterns: nested loops, sentinel loops, state machines, finite automata, fast/slow pointers, two-pointer, binary search loops

2) Basic examples + tips
If / If-Else
if (x > 0) {
    System.out.println("positive");
} else if (x == 0) {
    System.out.println("zero");
} else {
    System.out.println("negative");
}


Tip: Avoid duplicate conditions; prefer else if for mutually exclusive branches.

Ternary operator
String sign = (x >= 0) ? "non-negative" : "negative";


Tip: Use for simple conditional assignment only — readable concise code.

Switch (classic)
switch (day) {
    case 1: System.out.println("Mon"); break;
    case 2: System.out.println("Tue"); break;
    default: System.out.println("Unknown"); 
}

Enhanced switch (Java 12+ style)
String result = switch (day) {
    case 1 -> "Mon";
    case 2 -> "Tue";
    default -> "Unknown";
};

For, while, do-while
for (int i = 0; i < n; i++) { ... }
while (condition) { ... }
do { ... } while (condition); // runs body at least once

For-each
for (String s : list) { ... }


Pitfall: Can't remove from a collection while iterating with for-each — use iterator.

Break / Continue / Labeled break
outer:
for (int i=0;i<n;i++){
  for (int j=0;j<m;j++){
    if (found) break outer; // exits both loops
  }
}

3) Common interview / real-time problem patterns using control statements

Below are patterns + sample problems with code and complexity.

A — FizzBuzz (beginner)

Print rules using conditionals.

public class FizzBuzz {
    public static void main(String[] args) {
        int n = 15;
        for (int i = 1; i <= n; i++) {
            if (i % 15 == 0) System.out.println("FizzBuzz");
            else if (i % 3 == 0) System.out.println("Fizz");
            else if (i % 5 == 0) System.out.println("Buzz");
            else System.out.println(i);
        }
    }
}


Time: O(n), Space: O(1).

B — Reverse a string (in-place using char array) — common LeetCode easy

Shows loops and two-pointer.

public class ReverseString {
    public static void reverse(char[] s) {
        int i = 0, j = s.length - 1;
        while (i < j) {
            char t = s[i]; s[i++] = s[j]; s[j--] = t;
        }
    }
    public static void main(String[] args) {
        char[] arr = "hello".toCharArray();
        reverse(arr);
        System.out.println(new String(arr)); // "olleh"
    }
}


Time O(n), Space O(1).

C — Two Sum (pattern: loop + hashmap) — typical leetcode (control statements + collections)

Uses loops + early return.

import java.util.*;

public class TwoSum {
    public static int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            int need = target - nums[i];
            if (map.containsKey(need)) {
                return new int[]{map.get(need), i};
            }
            map.put(nums[i], i);
        }
        return new int[]{-1, -1}; // not found
    }

    public static void main(String[] args) {
        int[] ans = twoSum(new int[]{2,7,11,15}, 9);
        System.out.println(Arrays.toString(ans)); // [0,1]
    }
}


Time O(n), Space O(n).

D — Check palindrome number (fast/slow pointers or reversing half)

Classic: don't convert to string (loop control + math).

public class PalindromeNumber {
    public static boolean isPalindrome(int x) {
        if (x < 0 || (x % 10 == 0 && x != 0)) return false;
        int reverted = 0;
        while (x > reverted) {
            reverted = reverted * 10 + x % 10;
            x /= 10;
        }
        return x == reverted || x == reverted / 10;
    }
    public static void main(String[] args) {
        System.out.println(isPalindrome(121)); // true
    }
}


Time O(log10(n)), Space O(1).

E — Binary Search (loop version) — must know loop invariants
public class BinarySearch {
    public static int bs(int[] a, int target) {
        int l = 0, r = a.length - 1;
        while (l <= r) {
            int mid = l + (r - l) / 2;
            if (a[mid] == target) return mid;
            else if (a[mid] < target) l = mid + 1;
            else r = mid - 1;
        }
        return -1;
    }
}


Tip: prefer l + (r-l)/2 to prevent overflow.

F — Remove duplicates from sorted array (in-place, two pointers)
public class RemoveDuplicates {
    public static int removeDuplicates(int[] nums) {
        if (nums.length == 0) return 0;
        int i = 0;
        for (int j = 1; j < nums.length; j++) {
            if (nums[j] != nums[i]) {
                nums[++i] = nums[j];
            }
        }
        return i + 1;
    }
}


Time O(n), Space O(1).

G — Find first non-repeating char in string (count + loop)
public class FirstUniqueChar {
    public static int firstUniqChar(String s) {
        int[] cnt = new int[256];
        for (char c : s.toCharArray()) cnt[c]++;
        for (int i = 0; i < s.length(); i++)
            if (cnt[s.charAt(i)] == 1) return i;
        return -1;
    }
}

4) Advanced control techniques & patterns
1. Labeled break/continue — useful when you must break out of nested loops:
outer:
for (...) {
  for (...) {
    if (cond) break outer;
  }
}

2. State machines — use switch or state variables to parse streaming input

Example: parse a small tokenizer or validate a format using a state variable and switch.

3. Short-circuit logic — && and ||

Evaluate left-to-right; stop early. Use for null checks:

if (obj != null && obj.isReady()) { ... } // safe

4. Loop invariants & correctness

When writing loops, reason about:

Initialization (true before first iteration)

Condition (keeps loop valid)

Update (progress towards termination)

5. Efficient early returns

Return as soon as you can to avoid needless work (common in interviews).

6. Avoiding off-by-one

Prefer clear boundaries: for (int i=0;i<n;i++) vs i<=n-1.

7. Sentinel loops / input-driven loops
Scanner sc = new Scanner(System.in);
String line;
while (!(line = sc.nextLine()).equals("QUIT")) {
    // process line
}

8. Concurrency-related control

Simple note: synchronized / volatile affect control flow by ordering operations — beyond these examples, concurrency requires extra care.

5) Real-time / system-style examples
Example: Simple CLI menu (control statements + input parsing)
import java.util.Scanner;
public class MenuApp {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        while (true) {
            System.out.println("1) Add  2) View  3) Exit");
            System.out.print("Choose: ");
            int choice = -1;
            try { choice = Integer.parseInt(sc.nextLine()); } 
            catch (NumberFormatException e) { System.out.println("Invalid"); continue; }
            switch (choice) {
                case 1: System.out.println("Add item"); break;
                case 2: System.out.println("View items"); break;
                case 3: System.out.println("Exiting"); sc.close(); return;
                default: System.out.println("Unknown choice");
            }
        }
    }
}

Example: Validate input format with state machine

Parse simple CSV line with quoted fields using for + state variable — helpful for streaming or large files.

6) Common pitfalls & debugging tips

Infinite loops — ensure loop variable changes; use logging or breakpoints.

Off-by-one — test boundary cases (n=0, n=1, large n).

Concurrent modification — don't modify collection in for-each; use Iterator.remove() or ListIterator.

Switch fall-through — remember break in classic switch; or use modern switch expressions.

Null checks — use Objects.requireNonNull or if (o!=null && ... ) to avoid NPE.

Floating point equality — don't use ==; use epsilon.

Performance — prefer StringBuilder inside loops for string concatenation.

7) Advanced interview/contest examples (with explanations)
Example — Sliding window: Longest substring without repeating characters (LeetCode 3)

Uses two-pointer + loop control; O(n).

import java.util.*;

public class LongestUniqueSubstr {
    public static int lengthOfLongestSubstring(String s) {
        int[] last = new int[256];
        Arrays.fill(last, -1);
        int res = 0, start = 0;
        for (int i = 0; i < s.length(); i++) {
            start = Math.max(start, last[s.charAt(i)] + 1);
            res = Math.max(res, i - start + 1);
            last[s.charAt(i)] = i;
        }
        return res;
    }
    public static void main(String[] args) {
        System.out.println(lengthOfLongestSubstring("abcabcbb")); // 3
    }
}

Example — Fast & Slow Pointer: Detect cycle in linked list (LeetCode 141)
class ListNode { int val; ListNode next; ListNode(int v){val=v;} }
public class CycleDetect {
    public boolean hasCycle(ListNode head) {
        ListNode slow = head, fast = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
            if (slow == fast) return true;
        }
        return false;
    }
}

8) Practice problems to work through (progression)

FizzBuzz — conditionals & loops (easy).

Reverse a string / array in-place (easy).

Two Sum — loop + hashmap (easy).

Binary search in rotated array (medium) — attention to conditions.

Longest substring without repeating characters (medium) — sliding window.

Detect cycle in linked list (easy/medium) — two pointers.

Merge intervals (sorting + loop) — careful pointer movement.

Regex-based input validation — switch + state machine (advanced).

9) Short reference cheatsheet (when to use what)

Use if/else for boolean condition branching.

Use switch when branching by discrete known values (enums, ints, strings).

Use for when you need index or fixed iteration count.

Use enhanced for for simple iteration over collections/arrays.

Use while for unknown number of iterations until a condition changes.

Use do-while when the body must run at least once.

Use break to exit loops early; continue to skip current iteration.

Use labeled breaks for nested-loop exits (sparingly).
=======
here’s a complete, practical guide to Java control statements from basic → advanced, with real-time / interview-style problems (LeetCode/HackerRank style), explanations, and ready-to-run Java code. I’ll show patterns, pitfalls, and complexity notes so you can use these constructs in real problems.

1) Quick overview — what are control statements?

Control statements let you choose execution paths and repeat actions:

Decision: if, if-else, if-else if-..., ternary ?:, switch (classic + modern switch expressions)

Loops: for, enhanced for (for-each), while, do-while

Loop control: break, continue, labeled break/continue, return

Short-circuit & boolean control: &&, || (order matters)

Other patterns: nested loops, sentinel loops, state machines, finite automata, fast/slow pointers, two-pointer, binary search loops

2) Basic examples + tips
If / If-Else
if (x > 0) {
    System.out.println("positive");
} else if (x == 0) {
    System.out.println("zero");
} else {
    System.out.println("negative");
}


Tip: Avoid duplicate conditions; prefer else if for mutually exclusive branches.

Ternary operator
String sign = (x >= 0) ? "non-negative" : "negative";


Tip: Use for simple conditional assignment only — readable concise code.

Switch (classic)
switch (day) {
    case 1: System.out.println("Mon"); break;
    case 2: System.out.println("Tue"); break;
    default: System.out.println("Unknown"); 
}

Enhanced switch (Java 12+ style)
String result = switch (day) {
    case 1 -> "Mon";
    case 2 -> "Tue";
    default -> "Unknown";
};

For, while, do-while
for (int i = 0; i < n; i++) { ... }
while (condition) { ... }
do { ... } while (condition); // runs body at least once

For-each
for (String s : list) { ... }


Pitfall: Can't remove from a collection while iterating with for-each — use iterator.

Break / Continue / Labeled break
outer:
for (int i=0;i<n;i++){
  for (int j=0;j<m;j++){
    if (found) break outer; // exits both loops
  }
}

3) Common interview / real-time problem patterns using control statements

Below are patterns + sample problems with code and complexity.

A — FizzBuzz (beginner)

Print rules using conditionals.

public class FizzBuzz {
    public static void main(String[] args) {
        int n = 15;
        for (int i = 1; i <= n; i++) {
            if (i % 15 == 0) System.out.println("FizzBuzz");
            else if (i % 3 == 0) System.out.println("Fizz");
            else if (i % 5 == 0) System.out.println("Buzz");
            else System.out.println(i);
        }
    }
}


Time: O(n), Space: O(1).

B — Reverse a string (in-place using char array) — common LeetCode easy

Shows loops and two-pointer.

public class ReverseString {
    public static void reverse(char[] s) {
        int i = 0, j = s.length - 1;
        while (i < j) {
            char t = s[i]; s[i++] = s[j]; s[j--] = t;
        }
    }
    public static void main(String[] args) {
        char[] arr = "hello".toCharArray();
        reverse(arr);
        System.out.println(new String(arr)); // "olleh"
    }
}


Time O(n), Space O(1).

C — Two Sum (pattern: loop + hashmap) — typical leetcode (control statements + collections)

Uses loops + early return.

import java.util.*;

public class TwoSum {
    public static int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            int need = target - nums[i];
            if (map.containsKey(need)) {
                return new int[]{map.get(need), i};
            }
            map.put(nums[i], i);
        }
        return new int[]{-1, -1}; // not found
    }

    public static void main(String[] args) {
        int[] ans = twoSum(new int[]{2,7,11,15}, 9);
        System.out.println(Arrays.toString(ans)); // [0,1]
    }
}


Time O(n), Space O(n).

D — Check palindrome number (fast/slow pointers or reversing half)

Classic: don't convert to string (loop control + math).

public class PalindromeNumber {
    public static boolean isPalindrome(int x) {
        if (x < 0 || (x % 10 == 0 && x != 0)) return false;
        int reverted = 0;
        while (x > reverted) {
            reverted = reverted * 10 + x % 10;
            x /= 10;
        }
        return x == reverted || x == reverted / 10;
    }
    public static void main(String[] args) {
        System.out.println(isPalindrome(121)); // true
    }
}


Time O(log10(n)), Space O(1).

E — Binary Search (loop version) — must know loop invariants
public class BinarySearch {
    public static int bs(int[] a, int target) {
        int l = 0, r = a.length - 1;
        while (l <= r) {
            int mid = l + (r - l) / 2;
            if (a[mid] == target) return mid;
            else if (a[mid] < target) l = mid + 1;
            else r = mid - 1;
        }
        return -1;
    }
}


Tip: prefer l + (r-l)/2 to prevent overflow.

F — Remove duplicates from sorted array (in-place, two pointers)
public class RemoveDuplicates {
    public static int removeDuplicates(int[] nums) {
        if (nums.length == 0) return 0;
        int i = 0;
        for (int j = 1; j < nums.length; j++) {
            if (nums[j] != nums[i]) {
                nums[++i] = nums[j];
            }
        }
        return i + 1;
    }
}


Time O(n), Space O(1).

G — Find first non-repeating char in string (count + loop)
public class FirstUniqueChar {
    public static int firstUniqChar(String s) {
        int[] cnt = new int[256];
        for (char c : s.toCharArray()) cnt[c]++;
        for (int i = 0; i < s.length(); i++)
            if (cnt[s.charAt(i)] == 1) return i;
        return -1;
    }
}

4) Advanced control techniques & patterns
1. Labeled break/continue — useful when you must break out of nested loops:
outer:
for (...) {
  for (...) {
    if (cond) break outer;
  }
}

2. State machines — use switch or state variables to parse streaming input

Example: parse a small tokenizer or validate a format using a state variable and switch.

3. Short-circuit logic — && and ||

Evaluate left-to-right; stop early. Use for null checks:

if (obj != null && obj.isReady()) { ... } // safe

4. Loop invariants & correctness

When writing loops, reason about:

Initialization (true before first iteration)

Condition (keeps loop valid)

Update (progress towards termination)

5. Efficient early returns

Return as soon as you can to avoid needless work (common in interviews).

6. Avoiding off-by-one

Prefer clear boundaries: for (int i=0;i<n;i++) vs i<=n-1.

7. Sentinel loops / input-driven loops
Scanner sc = new Scanner(System.in);
String line;
while (!(line = sc.nextLine()).equals("QUIT")) {
    // process line
}

8. Concurrency-related control

Simple note: synchronized / volatile affect control flow by ordering operations — beyond these examples, concurrency requires extra care.

5) Real-time / system-style examples
Example: Simple CLI menu (control statements + input parsing)
import java.util.Scanner;
public class MenuApp {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        while (true) {
            System.out.println("1) Add  2) View  3) Exit");
            System.out.print("Choose: ");
            int choice = -1;
            try { choice = Integer.parseInt(sc.nextLine()); } 
            catch (NumberFormatException e) { System.out.println("Invalid"); continue; }
            switch (choice) {
                case 1: System.out.println("Add item"); break;
                case 2: System.out.println("View items"); break;
                case 3: System.out.println("Exiting"); sc.close(); return;
                default: System.out.println("Unknown choice");
            }
        }
    }
}

Example: Validate input format with state machine

Parse simple CSV line with quoted fields using for + state variable — helpful for streaming or large files.

6) Common pitfalls & debugging tips

Infinite loops — ensure loop variable changes; use logging or breakpoints.

Off-by-one — test boundary cases (n=0, n=1, large n).

Concurrent modification — don't modify collection in for-each; use Iterator.remove() or ListIterator.

Switch fall-through — remember break in classic switch; or use modern switch expressions.

Null checks — use Objects.requireNonNull or if (o!=null && ... ) to avoid NPE.

Floating point equality — don't use ==; use epsilon.

Performance — prefer StringBuilder inside loops for string concatenation.

7) Advanced interview/contest examples (with explanations)
Example — Sliding window: Longest substring without repeating characters (LeetCode 3)

Uses two-pointer + loop control; O(n).

import java.util.*;

public class LongestUniqueSubstr {
    public static int lengthOfLongestSubstring(String s) {
        int[] last = new int[256];
        Arrays.fill(last, -1);
        int res = 0, start = 0;
        for (int i = 0; i < s.length(); i++) {
            start = Math.max(start, last[s.charAt(i)] + 1);
            res = Math.max(res, i - start + 1);
            last[s.charAt(i)] = i;
        }
        return res;
    }
    public static void main(String[] args) {
        System.out.println(lengthOfLongestSubstring("abcabcbb")); // 3
    }
}

Example — Fast & Slow Pointer: Detect cycle in linked list (LeetCode 141)
class ListNode { int val; ListNode next; ListNode(int v){val=v;} }
public class CycleDetect {
    public boolean hasCycle(ListNode head) {
        ListNode slow = head, fast = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
            if (slow == fast) return true;
        }
        return false;
    }
}

8) Practice problems to work through (progression)

FizzBuzz — conditionals & loops (easy).

Reverse a string / array in-place (easy).

Two Sum — loop + hashmap (easy).

Binary search in rotated array (medium) — attention to conditions.

Longest substring without repeating characters (medium) — sliding window.

Detect cycle in linked list (easy/medium) — two pointers.

Merge intervals (sorting + loop) — careful pointer movement.

Regex-based input validation — switch + state machine (advanced).

9) Short reference cheatsheet (when to use what)

Use if/else for boolean condition branching.

Use switch when branching by discrete known values (enums, ints, strings).

Use for when you need index or fixed iteration count.

Use enhanced for for simple iteration over collections/arrays.

Use while for unknown number of iterations until a condition changes.

Use do-while when the body must run at least once.

Use break to exit loops early; continue to skip current iteration.

Use labeled breaks for nested-loop exits (sparingly).
>>>>>>> 3b36c0597166863e15545dafb8ceb347a40d878a
