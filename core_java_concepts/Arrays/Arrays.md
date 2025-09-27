here’s a complete guide to Arrays in Java, from basic → advanced, including practical examples, concepts, and real-world/competitive coding problems.

🔹 1. What is an Array in Java?

An array is a fixed-size container that holds elements of the same data type, stored in contiguous memory locations.

🧱 Syntax:
int[] arr = new int[5];           // declares an int array of size 5
int[] arr2 = {1, 2, 3, 4, 5};     // array initializer

🔹 2. Declaring, Creating & Initializing Arrays
// Declaration
int[] numbers;
String[] names;

// Creation
numbers = new int[3];   // default initialized to 0
names = new String[3];  // default initialized to null

// Initialization
numbers[0] = 10;
numbers[1] = 20;
numbers[2] = 30;

🔹 3. Default values of Arrays
Data Type	Default Value
int, long	0
double, float	0.0
boolean	false
char	'\u0000'
Object/String	null
🔹 4. Array Traversal
✅ Using for loop:
for (int i = 0; i < arr.length; i++) {
    System.out.println(arr[i]);
}

✅ Using enhanced for-each loop:
for (int num : arr) {
    System.out.println(num);
}

🔹 5. Multidimensional Arrays
✅ 2D Array:
int[][] matrix = new int[3][4];  // 3 rows, 4 columns

int[][] identity = {
    {1, 0, 0},
    {0, 1, 0},
    {0, 0, 1}
};

System.out.println(identity[1][1]);  // Output: 1

🔹 6. Arrays and Constructors

You can pass arrays into constructors:

public class Student {
    String name;
    int[] marks;

    public Student(String name, int[] marks) {
        this.name = name;
        this.marks = marks;
    }

    public void printMarks() {
        for (int mark : marks) {
            System.out.print(mark + " ");
        }
    }
}

// Usage
int[] m = {85, 90, 78};
Student s = new Student("John", m);
s.printMarks();  // Output: 85 90 78

🔹 7. Arrays Utility Methods (java.util.Arrays)
import java.util.Arrays;

int[] a = {5, 2, 9, 1};

Arrays.sort(a);                // Sort the array
int idx = Arrays.binarySearch(a, 2); // Search in sorted array
int[] copy = Arrays.copyOf(a, 3);    // Copy first 3 elements

System.out.println(Arrays.toString(a));  // [1, 2, 5, 9]

🔹 8. Real-Time / Interview Problems
✅ 1. Reverse an array (in-place)
public static void reverse(int[] arr) {
    int i = 0, j = arr.length - 1;
    while (i < j) {
        int temp = arr[i];
        arr[i++] = arr[j];
        arr[j--] = temp;
    }
}

✅ 2. Find max and min in array
int max = Integer.MIN_VALUE, min = Integer.MAX_VALUE;
for (int num : arr) {
    if (num > max) max = num;
    if (num < min) min = num;
}

✅ 3. Remove duplicates from sorted array (LeetCode)
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

✅ 4. Move all zeros to the end (LeetCode)
public static void moveZeroes(int[] nums) {
    int i = 0;
    for (int j = 0; j < nums.length; j++) {
        if (nums[j] != 0) {
            int temp = nums[i];
            nums[i++] = nums[j];
            nums[j] = temp;
        }
    }
}

✅ 5. Kadane's Algorithm - Max subarray sum
public static int maxSubArray(int[] nums) {
    int maxSoFar = nums[0], curr = nums[0];
    for (int i = 1; i < nums.length; i++) {
        curr = Math.max(nums[i], curr + nums[i]);
        maxSoFar = Math.max(maxSoFar, curr);
    }
    return maxSoFar;
}

✅ 6. Sliding Window - Max sum of size k
public static int maxSum(int[] arr, int k) {
    int sum = 0, max = 0;
    for (int i = 0; i < k; i++) sum += arr[i];
    max = sum;
    for (int i = k; i < arr.length; i++) {
        sum += arr[i] - arr[i - k];
        max = Math.max(max, sum);
    }
    return max;
}

✅ 7. Binary Search (classic)
public static int binarySearch(int[] arr, int target) {
    int low = 0, high = arr.length - 1;
    while (low <= high) {
        int mid = low + (high - low) / 2;
        if (arr[mid] == target) return mid;
        else if (arr[mid] < target) low = mid + 1;
        else high = mid - 1;
    }
    return -1;
}

🔹 9. Array vs ArrayList (Important)
Feature	Array	ArrayList
Size	Fixed	Dynamic
Type	Primitive & Obj	Objects only
Length	arr.length	list.size()
Can remove/add	No	Yes
🔹 10. Final Tips

Use Arrays.toString(arr) for debugging arrays.

Use Arrays.sort(arr) for sorting.

Be careful of ArrayIndexOutOfBoundsException.

For large arrays, prefer primitive arrays for performance.

Use Arrays.equals() and Arrays.deepEquals() to compare arrays.
