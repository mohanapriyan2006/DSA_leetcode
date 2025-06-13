# *DSA*
-----------

# Count Digits (GeeksForGeeks)
Difficulty: Easy
Given a positive integer n, count the number of digits in n that divide n evenly (i.e., without leaving a remainder). Return the total number of such digits.

A digit d of n divides n evenly if the remainder when n is divided by d is 0 (n % d == 0).
Digits of n should be checked individually. If a digit is 0, it should be ignored because division by 0 is undefined.

Examples :

Input: n = 12
Output: 2
Explanation: 1, 2 when both divide 12 leaves remainder 0.
Input: n = 2446
Output: 1
Explanation: Here among 2, 4, 6 only 2 divides 2446 evenly while 4 and 6 do not.
Input: n = 23
Output: 0
Explanation: 2 and 3, none of them divide 23 evenly.

```java []
class Solution {
    static int evenlyDivides(int n) {
        int dp = n;
        int rem;
        int ans = 0;
        while(n>0){
            rem = n % 10;
            if(rem != 0 && dp % rem == 0){
                ans++;
            }
            n/=10;
        }
        
        return ans;
    }
}
```

---


# 7. Reverse Integer (leetcode)

Medium

Given a signed 32-bit integer x, return x with its digits reversed. If reversing x causes the value to go outside the signed 32-bit integer range [-231, 231 - 1], then return 0.

Assume the environment does not allow you to store 64-bit integers (signed or unsigned).

 

Example 1:

Input: x = 123
Output: 321
Example 2:

Input: x = -123
Output: -321
Example 3:

Input: x = 120
Output: 21
 

Constraints:

-231 <= x <= 231 - 1

# Code
```java []
class Solution {
    public int reverse(int x) {

        long ans = 0;
        while(x != 0){
            ans = (ans * 10) + (x % 10);
            x /= 10;
        }

        return (ans < Integer.MIN_VALUE || ans > Integer.MAX_VALUE) ? 0 : (int)ans;
    }
}
```

---

# 9. Palindrome Number (leetCode)
Easy

Given an integer x, return true if x is a 
palindrome
, and false otherwise.

 

Example 1:

Input: x = 121
Output: true
Explanation: 121 reads as 121 from left to right and from right to left.
Example 2:

Input: x = -121
Output: false
Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.
Example 3:

Input: x = 10
Output: false
Explanation: Reads 01 from right to left. Therefore it is not a palindrome.
 

Constraints:

-231 <= x <= 231 - 1

# Code
```java []
class Solution {
    public boolean isPalindrome(int x) {
        
        int d = x;

        int sum = 0;
        while(d>0){
            int rem = d%10;
            sum = (sum * 10) + rem;
            d/=10;
        }

        if(sum == x)
            return true;
        
        return false;
    }
}
```

---

# Given two integers a and b, write a function lcmAndGcd() to compute their LCM and GCD. The function inputs two integers a and b and returns a list containing their LCM and GCD. (GeeksForGeeks)

Examples:

Input: a = 5 , b = 10
Output: [10, 5]
Explanation: LCM of 5 and 10 is 10, while their GCD is 5.
Input: a = 14 , b = 8
Output: [56, 2]
Explanation: LCM of 14 and 8 is 56, while their GCD is 2.
Input: a = 1 , b = 1
Output: [1, 1]
Explanation: LCM of 1 and 1 is 1, while their GCD is 1.
Expected Time Complexity: O(log(min(a, b))
Expected Auxiliary Space: O(1)

Constraints:
1 <= a, b <= 109

# Code
```java []
class Solution {
    public static int GCD(int a,int b){
        if(b == 0) return a;
        return GCD(b , a % b);
    }
    
    public static int[] lcmAndGcd(int a, int b) {
        int[] ans = new int[2];
        int gcd = GCD(a,b);
        int lcm = (a * b)/gcd;
        ans[0] = lcm;
        ans[1] = gcd;
        
        return ans;
    }
}
```

---

# Check if a number is Armstrong Number or not

Problem Statement: Given an integer N, return true it is an Armstrong number otherwise return false.

An Amrstrong number is a number that is equal to the sum of its own digits each raised to the power of the number of digits.

## Example 1:
Input:N = 153
Output:True
Explanation: 13+53+33 = 1 + 125 + 27 = 153

## Example 2:
Input:N = 371
Output: True
Explanation: 33+53+13 = 27 + 343 + 1 = 371

## Optimal Approach
Algorithm / Intuition
To check if a number is an armstrong number, we can use the algorithm created in Extract Digits.

An Armstrong number, also known as a narcissistic number or plenary number, is a number that is equal to the sum of its own digits each raised to the power of the number of digits.

Number of digits: 3, 153 = 13+53+33

We extract the digits of the number, raise each digit to the power of the total number of digits in the number. Sum up all the results obtained and check if the sum equals to the original number.

Algorithm
Step 1:Calculate the number of digits in the input number and store it in k. Read more about this Approach here: Count Digits

Step 2: Initialise a variable sum to 0. This variable will store the sum of each digit raised to the power of number of digits in number.

Make a copy of the original number to store it in a temporary variable.
Step 3: Run a while loop with the condition n>0 and at each iteration:

Get the last digit of n by using the modulus operator % with 10 and store it in a temporary variable ld.
Add the digit ld raised to the power of k of the sum.
Update n by integer division with 10 effectively removing the last digit.
Step 4: After the loop, check if the original input number is equal to the sum of the digits raised to the power of the number of digits in the number.

If they are equal, return true indicating the number is an Armstrong number.
If they are not equal, return false indicating that the number is not an Armstrong number.

# Code
```java []
                            
import java.lang.Math;

public class ArmstrongNumber {
    // Function to check if a
    // number is an Armstrong number
    public static boolean isArmstrong(int num) {
        // Calculate the number of
        // digits in the given number
        int k = String.valueOf(num).length();
        // Initialize the sum of digits
        // raised to the power of k to 0
        int sum = 0;
        // Copy the value of the input
        // number to a temporary variable n
        int n = num;
        // Iterate through each
        // digit of the number
        while(n > 0){
            // Extract the last
            // digit of the number
            int ld = n % 10;
            // Add the digit raised to
            // the power of k to the sum
            sum += Math.pow(ld, k); 
            // Remove the last digit
            // from the number
            n = n / 10;
        }
        // Check if the sum of digits raised to
        // the power of k equals the original number
        return sum == num ? true : false;
    }

    public static void main(String[] args) {
        int number = 153;
        if (isArmstrong(number)) {
            System.out.println(number + " is an Armstrong number.");
        } else {
            System.out.println(number + " is not an Armstrong number.");
        }
    }
}
                            
```
---

# Print all Divisors of a given Number


Problem Statement: Given an integer N, return all divisors of N.

A divisor of an integer N is a positive integer that divides N without leaving a remainder. In other words, if N is divisible by another integer without any remainder, then that integer is considered a divisor of N.


## Example 1:
Input:N = 36
Output:[1, 2, 3, 4, 6, 9, 12, 18, 36]
Explanation: The divisors of 36 are 1, 2, 3, 4, 6, 9, 12, 18, 36.
## Example 2:
Input:N =12
Output: [1, 2, 3, 4, 6, 12]
Explanation: The divisors of 12 are 1, 2, 3, 4, 6, 12.


## Optimal Approach

Algorithm / Intuition
We can optimise the previous approach by using the property that for any non-negative integer n, if d is a divisor of n then n/d is also a divisor of n.

![image](https://assets.leetcode.com/users/images/b9c12c5c-c17c-4400-9629-df58affdae6b_1739207422.1479151.png)


This property is symmetric about the square root of n by traversing just the first half we can avoid redundant iteration and computations improving the efficiency of the algorithm.


Algorithm

Step 1: Initialise an array to store the divisors.

Step 2: Iterate from 1 to square root of n using a loop variable ‘i’. For each value of ‘i’:

Check if ‘i’ is a divisor of ‘n’ by checking if ‘n’ is divisible by ‘i’ without a remainder (‘n’%i == 0).
If i is a divisor, add it to the vectors of divisors.
If i is different from n/i add the counterpart divisor n/i to the vector of divisors.
Step 3: After the loop, return the array of divisors.

# Code
```java []
                                
import java.util.ArrayList;

public class Main {
    public static ArrayList<Integer> findDivisors(int n) {
        // Initialize an empty
        // ArrayList to store the divisors
        ArrayList<Integer> divisors = new ArrayList<>();

        // Iterate up to the square
        // root of n to find divisors
        // Calculate the square root of n
        int sqrtN = (int) Math.sqrt(n);

        // Loop from 1 to the
        // square root of n
        for (int i = 1; i <= sqrtN; ++i) {
            // Check if i divides n
            // without leaving a remainder
            if (n % i == 0) {
                // Add divisor i to the list
                divisors.add(i);

                // Add the counterpart divisor
                // if it's different from i
                if (i != n / i) {
                    // Add the counterpart
                    // divisor to the list
                    divisors.add(n / i);
                }
            }
        }

        // Return the list of divisors
        return divisors;
    }

    public static void main(String[] args) {
        int number = 12;
        ArrayList<Integer> divisors = findDivisors(number);

        System.out.print("Divisors of " + number + " are: ");
        for (int divisor : divisors) {
            System.out.print(divisor + " ");
        }
        System.out.println();
    }
}
```
---
# Problem Statement: Given an integer N, check whether it is prime or not. A prime number is a number that is only divisible by 1 and itself and the total number of divisors is 2.

### Example 1:
Input:N = 2
Output:True
Explanation: 2 is a prime number because it has two divisors: 1 and 2 (the number itself).
### Example 2:
Input:N =10
Output: False
Explanation: 10 is not prime, it is a composite number because it has 4 divisors: 1, 2, 5 and 10.

# Code
```java []
                                
import java.util.ArrayList;

public class Main {
    public static ArrayList<Integer> findDivisors(int n) {
        // Initialize an empty
        // ArrayList to store the divisors
        ArrayList<Integer> divisors = new ArrayList<>();

        // Iterate up to the square
        // root of n to find divisors
        // Calculate the square root of n
        int sqrtN = (int) Math.sqrt(n);

        // Loop from 1 to the
        // square root of n
        for (int i = 1; i <= sqrtN; ++i) {
            // Check if i divides n
            // without leaving a remainder
            if (n % i == 0) {
                // Add divisor i to the list
                divisors.add(i);

                // Add the counterpart divisor
                // if it's different from i
                if (i != n / i) {
                    // Add the counterpart
                    // divisor to the list
                    divisors.add(n / i);
                }
            }
        }

        // Return the list of divisors
        return divisors;
    }

    public static void main(String[] args) {
        int number = 12;
        ArrayList<Integer> divisors = findDivisors(number);

        System.out.print("Divisors of " + number + " are: ");
        for (int divisor : divisors) {
            System.out.print(divisor + " ");
        }
        System.out.println();
    }
}
```
---
# Print 1 To N Without Loop (GeeksForGeeks)
Print numbers from 1 to n without the help of loops. You only need to complete the function printNos() that takes n as a parameter and prints the number from 1 to n recursively.

Note: Don't print any newline, it will be added by the driver code.

### Examples:

Input: n = 10
Output: 1 2 3 4 5 6 7 8 9 10

Input: n = 5
Output: 1 2 3 4 5

Input: n = 1
Output: 1

Constraints:
1 <= n <= 1000

# Code
```java []
                                
class Solution {

    public void printNos(int n) {
        if(n == 0 ) return;
        printNos(n-1);
        System.out.print(n +" ");
    }
}

```
---

# Print GFG n times (GFG)
Difficulty: Easy

Print GFG n times without the loop.

### Example
Input:
5
Output:
GFG GFG GFG GFG GFG

Your Task:
This is a function problem. You only need to complete the function printGfg() that takes N as parameter and prints N times GFG recursively. Don't print newline, it will be added by the driver code.


Expected Time Complexity: O(N).
Expected Auxiliary Space: O(N) (Recursive).

Constraint:
1<=N<=1000
# Code
```java []
class Solution {

    void printGfg(int N) {
        if(N == 0) return;
        printGfg(N-1);
        System.out.print("GFG ");
    }
}
```
---
# Print N to 1 without loop (GFG)
Difficulty: Easy

Print numbers from N to 1 (space separated) without the help of loops.

### Example 1:

Input:
N = 10
Output: 10 9 8 7 6 5 4 3 2 1

Your Task:
This is a function problem. You only need to complete the function printNos() that takes N as parameter and prints number from N to 1 recursively. Don't print newline, it will be added by the driver code.


Expected Time Complexity: O(N).
Expected Auxiliary Space: O(N) (Recursive).

Constraint
1<=n<=1000

# Code
```java []
class Solution {

    void printNos(int N) {
        if(N==0) return;
        System.out.print(N+" ");
        printNos(N-1);
    }
}
```
---

# Sum of first n terms (GFG)
Difficulty: Basic

Given an integer n, calculate the sum of series 13 + 23 + 33 + 43 + … till n-th term.

### Examples:
Input: n = 5
Output: 225
Explanation: 13 + 23 + 33 + 43 + 53 = 225

Input: n = 7
Output: 784
Explanation: 13 + 23 + 33 + 43 + 53 + 63 + 73 = 784

Constraints:
1 <= n <= 200 

# Code
```java []
class Solution {
    int sumOfSeries(int n) {
        if(n==1) return n;
        return ((int)Math.pow(n,3) + sumOfSeries(n-1));
    }
}
```
---
# Factorials Less than or Equal to n (GFG)
Difficulty: Easy

A number n is called a factorial number if it is the factorial of a positive integer. For example, the first few factorial numbers are 1, 2, 6, 24, 120,
Given a number n, the task is to return the list/vector of the factorial numbers smaller than or equal to n.

### Examples:

Input: n = 3
Output: 1 2
Explanation: The first factorial number is 1 which is less than equal to n. The second number is 2 which is less than equal to n,but the third factorial number is 6 which is greater than n. So we print only 1 and 2.

Input: n = 6
Output: 1 2 6
Explanation: The first three factorial numbers are less than equal to n but the fourth factorial number 24 is greater than n. So we print only first three factorial numbers.

Constraints:
1<=n<=1018

# Code
```java []
class Solution {
    static ArrayList<Long> factorialNumbers(long n) {
        ArrayList<Long> ans = new ArrayList<>();
        
        long fact = 1;
        long num = 2;
        while(fact <= n){
            ans.add(fact);
            fact *= num++;
        }
        
        return ans;
    }
}
```
---
# Reverse an Array (GFG)
Difficulty: Easy

You are given an array of integers arr[]. Your task is to reverse the given array.

Note: Modify the array in place.

### Examples:

Input: arr = [1, 4, 3, 2, 6, 5]
Output: [5, 6, 2, 3, 4, 1]
Explanation: The elements of the array are 1 4 3 2 6 5. After reversing the array, the first element goes to the last position, the second element goes to the second last position and so on. Hence, the answer is 5 6 2 3 4 1.

Input: arr = [4, 5, 2]
Output: [2, 5, 4]
Explanation: The elements of the array are 4 5 2. The reversed array will be 2 5 4.

Input: arr = [1]
Output: [1]
Explanation: The array has only single element, hence the reversed array is same as the original.

Constraints:
1<=arr.size()<=105
0<=arr[i]<=105

# Code
```java []
class Solution {
    public void reverseArray(int arr[]) {
        int st = 0 ; int end = arr.length -1;
        while(st<end){
            int temp = arr[st];
            arr[st++] = arr[end];
            arr[end--] = temp;
            
        }
    }
}
```
---
# 125. Valid Palindrome (leetCode)
Solved
Easy

A phrase is a palindrome if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

Given a string s, return true if it is a palindrome, or false otherwise.

 

### Example 1:

Input: s = "A man, a plan, a canal: Panama"
Output: true
Explanation: "amanaplanacanalpanama" is a palindrome.

### Example 2:

Input: s = "race a car"
Output: false
Explanation: "raceacar" is not a palindrome.

### Example 3:

Input: s = " "
Output: true
Explanation: s is an empty string "" after removing non-alphanumeric characters.
Since an empty string reads the same forward and backward, it is a palindrome.
 

Constraints:

1 <= s.length <= 2 * 105
s consists only of printable ASCII characters.

# Code
```java []
class Solution {
    public boolean isPalindrome(String s) {
        int st = 0 ; int end = s.length() -1;
        while(st < end){
            while(st < end && !Character.isLetterOrDigit(s.charAt(st))){
                ++st;
            }
            while(st < end && !Character.isLetterOrDigit(s.charAt(end))){
                --end;
            }
            if( Character.toLowerCase(s.charAt(st)) != Character.toLowerCase(s.charAt(end)) ){
                return false;
            }
            ++st;
            --end;
        }

        return true;
    }
}
```
---
# 509. Fibonacci Number (leetCode)
Solved
Easy

The Fibonacci numbers, commonly denoted F(n) form a sequence, called the Fibonacci sequence, such that each number is the sum of the two preceding ones, starting from 0 and 1. That is,

F(0) = 0, F(1) = 1
F(n) = F(n - 1) + F(n - 2), for n > 1.
Given n, calculate F(n).

 

### Example 1:

Input: n = 2
Output: 1
Explanation: F(2) = F(1) + F(0) = 1 + 0 = 1.
Example 2:

Input: n = 3
Output: 2
Explanation: F(3) = F(2) + F(1) = 1 + 1 = 2.
Example 3:

Input: n = 4
Output: 3
Explanation: F(4) = F(3) + F(2) = 2 + 1 = 3.


# Code
```java []
class Solution {
    public int fib(int n) {
     if( n == 0){
        return 0;
     }   
     if( n == 1){
        return 1;
     }
     return fib(n-1) + fib(n-2);
    }
}
```
---
# Frequencies in a Limited Array (GFG)
Difficulty: Easy

You are given an array arr[] containing positive integers. The elements in the array arr[] range from 1 to n (where n is the size of the array), and some numbers may be repeated or absent. Your task is to count the frequency of all numbers in the range 1 to n and return an array of size n such that result[i] represents the frequency of the number i (1-based indexing).

### Examples

Input: arr[] = [2, 3, 2, 3, 5]
Output: [0, 2, 2, 0, 1]
Explanation: We have: 1 occurring 0 times, 2 occurring 2 times, 3 occurring 2 times, 4 occurring 0 times, and 5 occurring 1 time.

Input: arr[] = [3, 3, 3, 3]
Output: [0, 0, 4, 0]
Explanation: We have: 1 occurring 0 times, 2 occurring 0 times, 3 occurring 4 times, and 4 occurring 0 times.

Input: arr[] = [1]
Output: [1]
Explanation: We have: 1 occurring 1 time, and there are no other numbers between 1 and the size of the array.

Constraints:
1 ≤ arr.size() ≤ 106
1 ≤ arr[i] ≤ arr.size()


# Code
```java []
class Solution {
    // Function to count the frequency of all elements from 1 to N in the array.
    public List<Integer> frequencyCount(int[] arr) {
        Map<Integer,Integer> freq = new HashMap<>();
        List<Integer> ans = new ArrayList<>();
        
        for(int i=0 ; i<arr.length ; ++i){
            // freq.put(arr[i],freq.getOrDefault(arr[i],0)+1);
            freq.merge(arr[i],1,Integer::sum);
        }
        
        for(int i=0 ; i<arr.length ; ++i){
            if(freq.get(i+1) != null)
                ans.add(freq.get(i+1));
            else
                ans.add(0);
        }
        
        return ans;
    }
}

```
---
# Find the highest/lowest frequency element

Problem Statement: Given an array of size N. Find the highest and lowest frequency element.

Pre-requisite: Hashing Theory and  Counting frequencies of array elements

### Example 1:
Input: array[] = {10,5,10,15,10,5};
Output: 10 15
Explanation: The frequency of 10 is 3, i.e. the highest and the frequency of 15 is 1 i.e. the lowest.

### Example 2:

Input: array[] = {2,2,3,4,4,2};
Output: 2 3
Explanation: The frequency of 2 is 3, i.e. the highest and the frequency of 3 is 1 i.e. the lowest.

### Solution

##### Optimized approach(Using map):

We can use a map of value and frequency pair, in which we can easily update the frequency of an element if it is already present in the map, if it is not present in the map then insert it in the map with frequency as 1. After completing all the iterations, we will find the element with the highest frequency and the element with the lowest frequency.

The steps are as follows:

Take a unordered_map<int, int> / HashMap of <Integer, Integer> pair.
Use a for loop to iterate the array.
If the element is not present in the map then insert it with frequency 1, otherwise increase the existing frequency by 1.
After visiting the whole array, we will find the element with the highest frequency and the element with the lowest frequency by iterating the map.

# Code
```java []
import java.util.*;

public class Main {

    public static void main(String args[]) {

        int arr[] = {10, 5, 10, 15, 10, 5};
        int n = arr.length;
        Frequency(arr, n);
    }
    static void Frequency(int arr[], int n) {
        Map<Integer, Integer> map = new HashMap<>();

        for (int i = 0; i < n; i++) {
            if (map.containsKey(arr[i])) {
                map.put(arr[i], map.get(arr[i]) + 1);
            } else {
                map.put(arr[i], 1);
            }
        }

        int maxFreq = 0, minFreq = n;
        int maxEle = 0, minEle = 0;
        // Traverse through map and find the elements
        for (Map.Entry<Integer, Integer> entry : map.entrySet()) {
            int count = entry.getValue();
            int element = entry.getKey();

            if (count > maxFreq) {
                maxEle = element;
                maxFreq = count;
            }
            if (count < minFreq) {
                minEle = element;
                minFreq = count;
            }
        }

        System.out.println("The highest frequency element is: " + maxEle);
        System.out.println("The lowest frequency element is: " + minEle);
    }
} 

```
---
---
# *Sorting*
---


## Selection Sort (GFG)
Difficulty: Easy

Given an array arr, use selection sort to sort arr[] in increasing order.

### Examples :

Input: arr[] = [4, 1, 3, 9, 7]
Output: [1, 3, 4, 7, 9]
Explanation: Maintain sorted (in bold) and unsorted subarrays. Select 1. Array becomes 1 4 3 9 7. Select 3. Array becomes 1 3 4 9 7. Select 4. Array becomes 1 3 4 9 7. Select 7. Array becomes 1 3 4 7 9. Select 9. Array becomes 1 3 4 7 9.

Input: arr[] = [10, 9, 8, 7, 6, 5, 4, 3, 2, 1]
Output: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
Input: arr[] = [38, 31, 20, 14, 30]
Output: [14, 20, 30, 31, 38]

Constraints:
1 ≤ arr.size() ≤ 103
1 ≤ arr[i] ≤ 106

# Code
```java []
class Solution {
    void selectionSort(int[] arr) {
        for(int i=0 ; i<arr.length ; ++i){
            int min = i;
            for(int j = i + 1 ; j<arr.length ; ++j){
                if(arr[j]<arr[min]){
                    min = j;
                }
            }
            
            int temp = arr[i];
            arr[i] = arr[min];
            arr[min] = temp;
        }
    }
}
```
---

# Bubble Sort (GFG)
Difficulty: Easy

Given an array, arr[]. Sort the array using bubble sort algorithm.

### Examples :

Input: arr[] = [4, 1, 3, 9, 7]
Output: [1, 3, 4, 7, 9]

Input: arr[] = [10, 9, 8, 7, 6, 5, 4, 3, 2, 1]
Output: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

Input: arr[] = [1, 2, 3, 4, 5]
Output: [1, 2, 3, 4, 5]
Explanation: An array that is already sorted should remain unchanged after applying bubble sort.

Constraints:
1 <= arr.size() <= 103
1 <= arr[i] <= 103

# Code
```java []
class Solution {
    // Function to sort the array using bubble sort algorithm.
    public static void bubbleSort(int arr[]) {
        int n = arr.length;
        for(int i=n-1 ; i>0 ; --i){
            int didSwap = 0;
            for(int j=0 ; j<i ; ++j){
                if(arr[j] > arr[j+1]){
                    int temp = arr[j];
                    arr[j] = arr[j+1];
                    arr[j+1] = temp;
                    didSwap = 1;
                }
            }
            
            if(didSwap == 0 ){
                break;
            }
        }
    }
}

```
---
# Insertion Sort (GFG)
Difficulty: Easy

The task is to complete the insertsort() function which is used to implement Insertion Sort.

### Examples:

Input: arr[] = [4, 1, 3, 9, 7]
Output: [1, 3, 4, 7, 9]
Explanation: The sorted array will be [1, 3, 4, 7, 9].

Input: arr[] = [10, 9, 8, 7, 6, 5, 4, 3, 2, 1]
Output: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
Explanation: The sorted array will be [1, 2, 3, 4, 5, 6, 7, 8, 9, 10].

Input: arr[] = [4, 1, 9]
Output: [1, 4, 9]
Explanation: The sorted array will be [1, 4, 9].

Constraints:
1 <= arr.size() <= 1000
1 <= arr[i] <= 1000

# Code
```java []
class Solution {
    // Please change the array in-place
    public void insertionSort(int arr[]) {
        for(int i=1 ; i<arr.length ; ++i){
            int j = i;
            while(j>0 && arr[j-1] > arr[j]){
                int temp = arr[j-1];
                arr[j-1] = arr[j];
                arr[j] = temp;
                j--;
            }
        }
    }
}
```
---
# Merge Sort (GFG)
Difficulty: Medium

Given an array arr[], its starting position l and its ending position r. Sort the array using the merge sort algorithm.

### Examples:

Input: arr[] = [4, 1, 3, 9, 7]
Output: [1, 3, 4, 7, 9]

Input: arr[] = [10, 9, 8, 7, 6, 5, 4, 3, 2, 1]
Output: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

Input: arr[] = [1, 3 , 2]
Output: [1, 2, 3]

Constraints:
1 <= arr.size() <= 105
1 <= arr[i] <= 105

# Code
```java []

class Solution {
    
    private void merge(int arr[],int low, int mid,int high){
        List<Integer> temp = new ArrayList<>();
        int l = low;
        int r = mid+1;
        
        while( l<=mid && r<=high ){
            if(arr[l] <= arr[r]){
                temp.add(arr[l++]);
            }
            else{
                temp.add(arr[r++]);
            }
        }
        
        while(l<=mid){
            temp.add(arr[l++]);
        }
        
        while(r<=high){
            temp.add(arr[r++]);
        }
        
        for(int i=low ; i<=high ; ++i){
            arr[i] = temp.get(i-low);
        }
    }

    void mergeSort(int arr[], int low, int high) {
        if(low >= high) return;
        int mid = (low + high)/2;
        
        mergeSort(arr,low,mid);
        mergeSort(arr,mid+1,high);
        
        merge(arr,low,mid,high);
    }
}

```
---
# Bubble Sort using Recursive (GFG)
Difficulty: Easy

Given an array, arr[]. Sort the array using bubble sort algorithm.

### Examples :

Input: arr[] = [4, 1, 3, 9, 7]
Output: [1, 3, 4, 7, 9]

Input: arr[] = [10, 9, 8, 7, 6, 5, 4, 3, 2, 1]
Output: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

Input: arr[] = [1, 2, 3, 4, 5]
Output: [1, 2, 3, 4, 5]
Explanation: An array that is already sorted should remain unchanged after applying bubble sort.

Constraints:
1 <= arr.size() <= 103
1 <= arr[i] <= 103

# Code
```java []

class Solution {
    private static void bubble(int arr[],int n){
        if(n == 1) return;
        
        int didSwap = 0;
        
        for(int i=0 ; i<n-1 ; i++){
            if(arr[i] > arr[i+1]){
                int temp = arr[i];
                arr[i] = arr[i+1];
                arr[i+1] = temp;
                didSwap = 1;
            }
        }
        
        if(didSwap == 0) return;
        
        bubble(arr,n-1);
    }
    // Function to sort the array using bubble sort algorithm.
    public static void bubbleSort(int arr[]) {
        bubble(arr,arr.length);
    }
}
```
---

# Insertion Sort using Recursive (GFG)
Difficulty: Easy

The task is to complete the insertsort() function which is used to implement Insertion Sort.

### Examples:

Input: arr[] = [4, 1, 3, 9, 7]
Output: [1, 3, 4, 7, 9]
Explanation: The sorted array will be [1, 3, 4, 7, 9].

Input: arr[] = [10, 9, 8, 7, 6, 5, 4, 3, 2, 1]
Output: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
Explanation: The sorted array will be [1, 2, 3, 4, 5, 6, 7, 8, 9, 10].

Input: arr[] = [4, 1, 9]
Output: [1, 4, 9]
Explanation: The sorted array will be [1, 4, 9].

Constraints:
1 <= arr.size() <= 1000
1 <= arr[i] <= 1000

# Code
```java []

class Solution {
    private static void insert(int arr[] , int i , int n){
        if( i== n ) return;
        int j = i;
        while(j>0 && arr[j-1] > arr[j]){
            int temp = arr[j-1];
            arr[j-1] = arr[j];
            arr[j--] = temp;
        }
        
        insert(arr,++i,n);
    }
    
    public void insertionSort(int arr[]) {
        insert(arr,1,arr.length);
    }
}

```
---
# Highest Occurring Element in an Array
Easy

Given an array of n integers, find the most frequent element in it i.e., the element that occurs the maximum number of times. If there are multiple elements that appear a maximum number of times, find the smallest of them.

### Examples:

Input: arr = [1, 2, 2, 3, 3, 3] <br/>

Output: 3 <br/>

Explanation: The number 3 appears the most (3 times). It is the most frequent element. <br/>


Input: arr = [4, 4, 5, 5, 6] <br/>

Output: 4 <br/>

Explanation: Both 4 and 5 appear twice, but 4 is smaller. So, 4 is the most frequent element. <br/>


```cpp []
class Solution {
public:
    int mostFrequentElement(vector<int>& nums) {
        unordered_map<int,int> mp;
        for(int i =0 ; i<nums.size() ; ++i){
            mp[nums[i]]++;
        }
        int maxEle = 0;
        int maxFreq = 0;
        for(auto it:mp){
            int curEle = it.first;
            int curFreq = it.second;
            if(maxFreq < curFreq) {
                maxFreq = curFreq;
                maxEle = curEle;
            }
        }

        return maxEle;
    }
};
```

----

# Quick Sort -> [link](https://www.geeksforgeeks.org/problems/quick-sort/1)

Difficulty: Medium
Implement Quick Sort, a Divide and Conquer algorithm, to sort an array, arr[] in ascending order. Given an array, arr[], with starting index low and ending index high, complete the functions partition() and quickSort(). Use the last element as the pivot so that all elements less than or equal to the pivot come before it, and elements greater than the pivot follow it.

Note: The low and high are inclusive.

Examples:

Input: arr[] = [4, 1, 3, 9, 7]

Output: [1, 3, 4, 7, 9]

Explanation: After sorting, all elements are arranged in ascending order.


Input: arr[] = [2, 1, 6, 10, 4, 1, 3, 9, 7]

Output: [1, 1, 2, 3, 4, 6, 7, 9, 10]

Explanation: Duplicate elements (1) are retained in sorted order.


Input: arr[] = [5, 5, 5, 5]

Output: [5, 5, 5, 5]

Explanation: All elements are identical, so the array remains unchanged.


Constraints:
1 <= arr.size() <= 105
1 <= arr[i] <= 105

Expected Complexities
Time Complexity: O(n log n)
Auxiliary Space: O(log n)

Company Tags
VMWare Amazon Microsoft Samsung Hike Ola  Cabs Goldman Sachs Adobe SAP Labs Qualcomm HSBC Grofers Target Corporation


```cpp []
class Solution {
  public:
    void quickSort(vector<int>& arr, int low, int high) {
        if(low<high){
            int part = partition(arr,low,high);
            quickSort(arr,low,part-1);
            quickSort(arr,part+1,high);
        }
        
    }

  public:
    int partition(vector<int>& arr, int low, int high) {
        int pivot = arr[low];
        int i = low;
        int j = high;
        
        while(i<j){
            while(pivot >= arr[i] && i<high){
                i++;
            }
            while(pivot < arr[j] && j>low){
                j--;
            }
            
            if(i<j) swap(arr[i],arr[j]);
        }
        
        swap(arr[low],arr[j]);
        
        return j;
    }
};
```

----

# Largest Element in Array -> [Link](https://www.geeksforgeeks.org/problems/largest-element-in-array4009/1)

Difficulty: Basic

Given an array arr[]. The task is to find the largest element and return it.

Examples:

Input: arr[] = [1, 8, 7, 56, 90]
Output: 90
Explanation: The largest element of the given array is 90.

Input: arr[] = [5, 5, 5, 5]
Output: 5
Explanation: The largest element of the given array is 5.

Input: arr[] = [10]
Output: 10
Explanation: There is only one element which is the largest.

Constraints:
1 <= arr.size()<= 106
0 <= arr[i] <= 106

Expected Complexities
Time Complexity: O(n)
Auxiliary Space: O(1)

Company Tags
Infosys Oracle Wipro Morgan Stanley


```cpp []
#include<bits/stdc++.h>
class Solution {
  public:
    int largest(vector<int> &arr) {
        int m = arr[0];
        for(int i=1 ; i<arr.size() ; ++i){
            m = max(m,arr[i]);
        }
        return m;
    }
};
```

----

# 215. Kth Largest Element in an Array -> [Link](https://leetcode.com/problems/kth-largest-element-in-an-array/description/)

Medium

Given an integer array nums and an integer k, return the kth largest element in the array.

Note that it is the kth largest element in the sorted order, not the kth distinct element.

Can you solve it without sorting?

 

Example 1:

Input: nums = [3,2,1,5,6,4], k = 2
Output: 5
Example 2:

Input: nums = [3,2,3,1,2,4,5,5,6], k = 4
Output: 4
 

Constraints:

1 <= k <= nums.length <= 105
-104 <= nums[i] <= 104


# Code
```cpp []
class Solution {
public:
    int findKthLargest(vector<int>& arr, int k) {
        priority_queue<int , vector<int> , greater<>> minheap;

        for(const int n:arr){
            minheap.push(n);
            if(minheap.size() > k) minheap.pop();
        }

        return minheap.top();
    }
};

```
----

# Check if array is sorted -> [Link](https://www.geeksforgeeks.org/problems/check-if-an-array-is-sorted0701/1)

Difficulty: Easy

Given an array arr[], check whether it is sorted in non-decreasing order. Return true if it is sorted otherwise false.

Examples:

Input: arr[] = [10, 20, 30, 40, 50]
Output: true
Explanation: The given array is sorted.

Input: arr[] = [90, 80, 100, 70, 40, 30]
Output: false
Explanation: The given array is not sorted.

Constraints:
1 ≤ arr.size ≤ 106
- 109 ≤ arr[i] ≤ 109

Expected Complexities
Time Complexity: O(n)
Auxiliary Space: O(1)

# Code
```cpp []
class Solution {
public:
    int findKthLargest(vector<int>& arr, int k) {
        priority_queue<int , vector<int> , greater<>> minheap;

        for(const int n:arr){
            minheap.push(n);
            if(minheap.size() > k) minheap.pop();
        }

        return minheap.top();
    }
};

```
----
