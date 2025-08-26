# *DSA* (*A2Z*)

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

# Bubble Sort [(GFG)](https://www.geeksforgeeks.org/problems/bubble-sort/1)
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
# Insertion Sort [(GFG)](https://www.geeksforgeeks.org/problems/insertion-sort/1)
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
# Bubble Sort using Recursive [(GFG)](https://www.geeksforgeeks.org/problems/bubble-sort/1)
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

# Insertion Sort using Recursive [(GFG)](https://www.geeksforgeeks.org/problems/insertion-sort/1)
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
-----------------------------------

# Array

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
# 1752. Check if Array Is Sorted and Rotated 
Easy

Given an array nums, return true if the array was originally sorted in non-decreasing order, then rotated some number of positions (including zero). Otherwise, return false.

There may be duplicates in the original array.

Note: An array A rotated by x positions results in an array B of the same length such that B[i] == A[(i+x) % A.length] for every valid index i.

Example 1:

Input: nums = [3,4,5,1,2] Output: true Explanation: [1,2,3,4,5] is the original sorted array. You can rotate the array by x = 3 positions to begin on the element of value 3: [3,4,5,1,2]. Example 2:

Input: nums = [2,1,3,4] Output: false Explanation: There is no sorted array once rotated that can make nums. Example 3:

Input: nums = [1,2,3] Output: true Explanation: [1,2,3] is the original sorted array. You can rotate the array by x = 0 positions (i.e. no rotation) to make nums.

Constraints:

1 <= nums.length <= 100 1 <= nums[i] <= 100

Code

```cpp []
class Solution {
public:
    bool check(vector<int>& nums) {
        int n = nums.size();
        int r = 0;
        for(int i=0 ; i<n ; ++i){
            if(nums[i] > nums[(i+1) % n] && ++r > 1) return false;
        }
        return true;
    }
};
```
----

# 26. Remove Duplicates from Sorted Array -> [LINK](https://leetcode.com/problems/remove-duplicates-from-sorted-array/description/)

Easy

Given an integer array nums sorted in non-decreasing order, remove the duplicates in-place such that each unique element appears only once. The relative order of the elements should be kept the same. Then return the number of unique elements in nums.

Consider the number of unique elements of nums to be k, to get accepted, you need to do the following things:

Change the array nums such that the first k elements of nums contain the unique elements in the order they were present in nums initially. The remaining elements of nums are not important as well as the size of nums.
Return k.
Custom Judge:

The judge will test your solution with the following code:

int[] nums = [...]; // Input array
int[] expectedNums = [...]; // The expected answer with correct length

int k = removeDuplicates(nums); // Calls your implementation

assert k == expectedNums.length;
for (int i = 0; i < k; i++) {
    assert nums[i] == expectedNums[i];
}
If all assertions pass, then your solution will be accepted.

 

Example 1:

Input: nums = [1,1,2]
Output: 2, nums = [1,2,_]
Explanation: Your function should return k = 2, with the first two elements of nums being 1 and 2 respectively.
It does not matter what you leave beyond the returned k (hence they are underscores).

Example 2:

Input: nums = [0,0,1,1,1,2,2,3,3,4]
Output: 5, nums = [0,1,2,3,4,_,_,_,_,_]
Explanation: Your function should return k = 5, with the first five elements of nums being 0, 1, 2, 3, and 4 respectively.
It does not matter what you leave beyond the returned k (hence they are underscores).
 

Constraints:

1 <= nums.length <= 3 * 104
-100 <= nums[i] <= 100
nums is sorted in non-decreasing order.

# Code
```cpp []
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        int i =0 ;
        for(int j = 1  ; j<nums.size() ; ++j){
            if(nums[i] != nums[j]){
                i++;
                nums[i] = nums[j];
            }
        }
        return i +1;
    }
};
```
----

# Rotate Array by One -> [LINK](https://www.geeksforgeeks.org/problems/cyclically-rotate-an-array-by-one2614/1) (GFG)
Difficulty: Basic

Given an array arr, rotate the array by one position in clockwise direction.

Examples:

Input: arr[] = [1, 2, 3, 4, 5]
Output: [5, 1, 2, 3, 4]
Explanation: If we rotate arr by one position in clockwise 5 come to the front and remaining those are shifted to the end.

Input: arr[] = [9, 8, 7, 6, 4, 2, 1, 3]
Output: [3, 9, 8, 7, 6, 4, 2, 1]
Explanation: After rotating clock-wise 3 comes in first position.

Constraints:
1<=arr.size()<=105
0<=arr[i]<=105

Expected Complexities
Time Complexity: O(n)
Auxiliary Space: O(1)

# Code
```cpp []
class Solution {
  public:
    void rotate(vector<int> &arr) {
        int n = arr.size();
        
       int temp = arr[n-1];
       
       for(int i = n - 2 ; i>=0 ; --i){
           arr[i + 1] = arr[i];
       }
       
       arr[0] = temp;
       
    }
};
```
----

# Rotate Array -> [GFG](https://www.geeksforgeeks.org/problems/rotate-array-by-n-elements-1587115621/1)
Difficulty: Medium

Given an array arr[]. Rotate the array to the left (counter-clockwise direction) by d steps, where d is a positive integer. Do the mentioned change in the array in place.

Note: Consider the array as circular.

Examples :

Input: arr[] = [1, 2, 3, 4, 5], d = 2
Output: [3, 4, 5, 1, 2]
Explanation: when rotated by 2 elements, it becomes 3 4 5 1 2.

Input: arr[] = [2, 4, 6, 8, 10, 12, 14, 16, 18, 20], d = 3
Output: [8, 10, 12, 14, 16, 18, 20, 2, 4, 6]
Explanation: when rotated by 3 elements, it becomes 8 10 12 14 16 18 20 2 4 6.

Input: arr[] = [7, 3, 9, 1], d = 9
Output: [3, 9, 1, 7]
Explanation: when we rotate 9 times, we'll get 3 9 1 7 as resultant array.

Constraints:
1 <= arr.size(), d <= 105
0 <= arr[i] <= 105


Company Tags
AmazonMicrosoftMAQ Software

# Code
```cpp []
class Solution {
    private:
    void reverse(vector<int>& arr,int l,int h){
        while(l<=h) swap(arr[l++],arr[h--]);
    }
  public:
    // Function to rotate an array by d elements in counter-clockwise direction.
    void rotateArr(vector<int>& a, int k) {
        int len = a.size();
        k = k%len;
        if(k<0){
          k = k+len;
        }
        reverse(a,0,k-1);
        reverse(a,k,len-1);
        reverse(a,0,len-1);
    }
};
```
----

# 283. Move Zeroes -> [LeetCode](https://leetcode.com/problems/move-zeroes/)

Easy

Given an integer array nums, move all 0's to the end of it while maintaining the relative order of the non-zero elements.

Note that you must do this in-place without making a copy of the array.

 

Example 1:

Input: nums = [0,1,0,3,12]
Output: [1,3,12,0,0]
Example 2:

Input: nums = [0]
Output: [0]
 

Constraints:

1 <= nums.length <= 104
-231 <= nums[i] <= 231 - 1
 

Follow up: Could you minimize the total number of operations done?

# Code
```cpp []
class Solution {
public:
    void moveZeroes(vector<int>& a) {

        int n = a.size();
        int i =0 ;

        for(const int n : a){
            if(n != 0){
            a[i++] = n;
            }
        }

        while(i<n){
            a[i++] = 0;
        }

    }
};
```

----

# Array Search -> [GFG](https://www.geeksforgeeks.org/problems/search-an-element-in-an-array-1587115621/1)
Difficulty: Basic

Given an array, arr of n integers, and an integer element x, find whether element x is present in the array. Return the index of the first occurrence of x in the array, or -1 if it doesn't exist.

Examples:

Input: arr[] = [1, 2, 3, 4], x = 3
Output: 2
Explanation: There is one test case with array as [1, 2, 3 4] and element to be searched as 3. Since 3 is present at index 2, the output is 2.

Input: arr[] = [10, 8, 30, 4, 5], x = 5
Output: 4
Explanation: For array [1, 2, 3, 4, 5], the element to be searched is 5 and it is at index 4. So, the output is 4.

Input: arr[] = [10, 8, 30], x = 6
Output: -1
Explanation: The element to be searched is 6 and its not present, so we return -1.

Expected Time Complexity: O(n).
Expected Auxiliary Space: O(1). 

Constraints:
1 <= arr.size <= 106
0 <= arr[i] <= 106
0 <= x <= 105

# Code
```cpp []
class Solution {
  public:
    int search(vector<int>& arr, int x) {
        for(int i=0 ; i<arr.size() ; ++i){
            if(arr[i] == x) return i;
        }
        return -1;
    }
};
```

----

# Union of two sorted arrays -> [TUF](https://takeuforward.org/plus/dsa/problems/union-of-two-sorted-arrays)

Easy

Given two sorted arrays nums1 and nums2, return an array that contains the union of these two arrays. The elements in the union must be in ascending order.
The union of two arrays is an array where all values are distinct and are present in either the first array, the second array, or both.


Examples:

Input: nums1 = [1, 2, 3, 4, 5], nums2 = [1, 2, 7]

Output: [1, 2, 3, 4, 5, 7]

Explanation: The elements 1, 2 are common to both, 3, 4, 5 are from nums1 and 7 is from nums2

Input: nums1 = [3, 4, 6, 7, 9, 9], nums2 = [1, 5, 7, 8, 8]

Output: [1, 3, 4, 5, 6, 7, 8, 9]

Explanation: The element 7 is common to both, 3, 4, 6, 9 are from nums1 and 1, 5, 8 is from nums2

```cpp []
class Solution {
public:
    vector<int> unionArray(vector<int>& nums1, vector<int>& nums2) {
        int n = nums1.size();
        int m = nums2.size();
        int i=0,j=0;

        vector<int> unionArr;

        while(i<n && j<m){
            if(nums1[i]<=nums2[j]){
                if(unionArr.size() == 0 || unionArr.back() != nums1[i]){
                    unionArr.push_back(nums1[i]);
                }
                i++;
            }else{
                if(unionArr.size() == 0 || unionArr.back() != nums2[j]){
                    unionArr.push_back(nums2[j]);
                }
                j++;
            }
        }

        while(i<n){
            if(unionArr.size() == 0 || unionArr.back() != nums1[i]){
                unionArr.push_back(nums1[i]);
            }
            i++;
        }

        while(j<m){
            if(unionArr.size() == 0 || unionArr.back() != nums2[j]){
                unionArr.push_back(nums2[j]);
            }
            j++;
        }

        return unionArr;

    }
};
```
-----

# 485. Max Consecutive Ones -> [LeetCode](https://leetcode.com/problems/max-consecutive-ones/description/)

Easy

Given a binary array nums, return the maximum number of consecutive 1's in the array.

 

Example 1:

Input: nums = [1,1,0,1,1,1]
Output: 3
Explanation: The first two digits or the last three digits are consecutive 1s. The maximum number of consecutive 1s is 3.

Example 2:

Input: nums = [1,0,1,1,0,1]
Output: 2
 

Constraints:

1 <= nums.length <= 105
nums[i] is either 0 or 1.

# Code
```cpp []
class Solution {
public:
    int findMaxConsecutiveOnes(vector<int>& nums) {
        int ans = 0;
        int n = nums.size();
        int count = 0;

        for(int i=0 ; i<n ; ++i){
            if(nums[i] == 1){
                count++;
            }else{
                count = 0;
            }
            ans = max(count,ans);
        }

        return ans;
    }
};
```
----

# Unique Number I -> [GFG](https://www.geeksforgeeks.org/problems/find-unique-number/1)
Difficulty: Easy

Given a unsorted array arr[] of positive integers having all the numbers occurring exactly twice, except for one number which will occur only once. Find the number occurring only once.

Examples :

Input: arr[] = [1, 2, 1, 5, 5]
Output: 2
Explanation: Since 2 occurs once, while other numbers occur twice, 2 is the answer.
Input: arr[] = [2, 30, 2, 15, 20, 30, 15]
Output: 20
Explanation: Since 20 occurs once, while other numbers occur twice, 20 is the answer.
Constraints
1 ≤  arr.size()  ≤ 106
0 ≤ arr[i] ≤ 109

Expected Complexities
Time Complexity: O(n)
Auxiliary Space: O(1)

# Code
```cpp []
class Solution {
  public:
    int findUnique(vector<int> &arr) {
        int n = arr.size();
        
        int xr = 0;
        
        for(int i =0 ; i<n ; ++i){
            xr ^= arr[i];
        }
        
        return xr;
        
    }
};
```
----

# Longest Subarray With Sum K -> [CodingNinja](https://www.naukri.com/code360/problems/longest-subarray-with-sum-k_6682399?leftPanelTabValue=PROBLEM)
Easy

You are given an array 'a' of size 'n' and an integer 'k'.
Find the length of the longest subarray of 'a' whose sum is equal to 'k'.


Example :
Input: ‘n’ = 7 ‘k’ = 3
‘a’ = [1, 2, 3, 1, 1, 1, 1]

Output: 3

Explanation: Subarrays whose sum = ‘3’ are:

[1, 2], [3], [1, 1, 1] and [1, 1, 1]

Here, the length of the longest subarray is 3, which is our final answer.
Detailed explanation ( Input/output format, Notes, Images )

Sample Input 1 :
7 3
1 2 3 1 1 1 1


Sample Output 1 :
3


Explanation Of Sample Input 1 :
Subarrays whose sum = ‘3’ are:
[1, 2], [3], [1, 1, 1] and [1, 1, 1]
Here, the length of the longest subarray is 3, which is our final answer.


Sample Input 2 :
4 2
1 2 1 3


Sample Output 2 :
1


Sample Input 3 :
5 2
2 2 4 1 2 


Sample Output 3 :
1


Expected time complexity :
The expected time complexity is O(n).


Constraints :
1 <= 'n' <= 5 * 10 ^ 6
1 <= 'k' <= 10^18
0 <= 'a[i]' <= 10 ^ 9

Time Limit: 1-second

# Code
```cpp []
#include<bits/stdc++.h>

int longestSubarrayWithSumK(vector<int> a, long long k) {
    map<long long,int> hashmap;
    long long sum = 0;
    int maxlen = 0;

    for(int i=0 ; i<a.size() ; ++i){
        sum += a[i];
        if(sum == k){
            maxlen = max(maxlen,i+1);
        }
        long long rem = sum - k;
        if(hashmap.find(rem) != hashmap.end()){
            int len = i - hashmap[rem];
            maxlen = max(len , maxlen);
        }
        if(hashmap.find(sum) == hashmap.end()){
            hashmap[sum] = i;
        }
    }

    return maxlen;
}
```
----

# 136. Single Number -> [LeetCode](https://leetcode.com/problems/single-number/description/)

Easy

Given a non-empty array of integers nums, every element appears twice except for one. Find that single one.

You must implement a solution with a linear runtime complexity and use only constant extra space.

 

Example 1:

Input: nums = [2,2,1]

Output: 1

Example 2:

Input: nums = [4,1,2,1,2]

Output: 4

Example 3:

Input: nums = [1]

Output: 1

 

Constraints:

1 <= nums.length <= 3 * 104
-3 * 104 <= nums[i] <= 3 * 104
Each element in the array appears twice except for one element which appears only once.


# Code
```cpp []
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int n = nums.size();
        int ans = 0;

        for(const int n:nums){
            ans ^= n;
        }

        return ans;
    }
};
```

----


# 2149. Rearrange Array Elements by Sign -> [LeetCode](https://leetcode.com/problems/rearrange-array-elements-by-sign/description/)
 
Medium

You are given a 0-indexed integer array nums of even length consisting of an equal number of positive and negative integers.

You should return the array of nums such that the the array follows the given conditions:

Every consecutive pair of integers have opposite signs.
For all integers with the same sign, the order in which they were present in nums is preserved.
The rearranged array begins with a positive integer.
Return the modified array after rearranging the elements to satisfy the aforementioned conditions.

 

Example 1:

Input: nums = [3,1,-2,-5,2,-4]
Output: [3,-2,1,-5,2,-4]
Explanation:
The positive integers in nums are [3,1,2]. The negative integers are [-2,-5,-4].
The only possible way to rearrange them such that they satisfy all conditions is [3,-2,1,-5,2,-4].
Other ways such as [1,-2,2,-5,3,-4], [3,1,2,-2,-5,-4], [-2,3,-5,1,-4,2] are incorrect because they do not satisfy one or more conditions.  


Example 2:

Input: nums = [-1,1]
Output: [1,-1]
Explanation:
1 is the only positive integer and -1 the only negative integer in nums.
So nums is rearranged to [1,-1].
 

Constraints:

2 <= nums.length <= 2 * 105
nums.length is even
1 <= |nums[i]| <= 105
nums consists of equal number of positive and negative integers.

# Code
```cpp []
class Solution {
public:
    vector<int> rearrangeArray(vector<int>& nums) {
        int n = nums.size();
        vector<int> ans(n,0);
        int pos = 0  , neg = 1;
        for(int i=0 ; i<n ; ++i){
            if(nums[i] > 0 ){
                ans[pos] = nums[i];
                pos += 2;
            }else{
                ans[neg] = nums[i];
                neg += 2;
            }
        }
        return ans;
    }
};
```

----------


## Alternate Positive Negative -> [GFG](https://www.geeksforgeeks.org/problems/array-of-alternate-ve-and-ve-nos1401/1)
Difficulty: Easy

Given an unsorted array arr containing both positive and negative numbers. Your task is to rearrange the array and convert it into an array of alternate positive and negative numbers without changing the relative order.

Note:
- Resulting array should start with a positive integer (0 will also be considered as a positive integer).
- If any of the positive or negative integers are exhausted, then add the remaining integers in the answer as it is by maintaining the relative order.
- The array may or may not have the equal number of positive and negative integers.

Examples:

Input: arr[] = [9, 4, -2, -1, 5, 0, -5, -3, 2]
Output: [9, -2, 4, -1, 5, -5, 0, -3, 2]
Explanation: The positive numbers are [9, 4, 5, 0, 2] and the negative integers are [-2, -1, -5, -3]. Since, we need to start with the positive integer first and then negative integer and so on (by maintaining the relative order as well), hence we will take 9 from the positive set of elements and then -2 after that 4 and then -1 and so on.


Input: arr[] = [-5, -2, 5, 2, 4, 7, 1, 8, 0, -8]
Output: [5, -5, 2, -2, 4, -8, 7, 1, 8, 0]
Explanation : The positive numbers are [5, 2, 4, 7, 1, 8, 0] and the negative integers are [-5,-2,-8]. According to the given conditions we will start from the positive integer 5 and then -5 and so on. After reaching -8 there are no negative elements left, so according to the given rule, we will add the remaining elements (in this case positive elements are remaining) as it in by maintaining the relative order.


Input: arr[] = [9, 5, -2, -1, 5, 0, -5, -3, 2]
Output: [9, -2, 5, -1, 5, -5, 0, -3, 2]
Explanation: The positive numbers are [9, 5, 5, 0, 2] and the negative integers are [-2, -1, -5, -3]. Since, we need to start with the positive integer first and then negative integer and so on (by maintaining the relative order as well), hence we will take 9 from the positive set of elements and then -2 after that 5 and then -1 and so on.


Constraints:

1 ≤ arr.size() ≤ 106
-106 ≤ arr[i] ≤ 106


Expected Complexities

Time Complexity: O(n)
Auxiliary Space: O(n)


Company Tags

PaytmVMWareAmazonMicrosoftIntuit


Topic Tags

ArraysData Structures



# Code
```cpp []
// User function template for C++
class Solution {
  public:
    void rearrange(vector<int> &arr) {
        
        vector<int> pos , neg;
        for(const int i:arr){
            if(i>=0) pos.push_back(i);
            else neg.push_back(i);
        }
        
        
        if(pos.size() > neg.size()){
            for(int i=0 ; i<neg.size() ; ++i){
                arr[i*2] = pos[i];
                arr[i*2+1] = neg[i];
            }
            int ind = neg.size() * 2;
            for(int i=neg.size() ; i<pos.size() ; ++i){
                arr[ind++] = pos[i];
            }
        }
        else{
            for(int i=0 ; i<pos.size() ; ++i){
                arr[i*2] = pos[i];
                arr[i*2+1] = neg[i];
            }
            int ind = pos.size() * 2;
            for(int i=pos.size() ; i<neg.size() ; ++i){
                arr[ind++] = neg[i];
            }
        }
    }
};
```

----------


# 31. Next Permutation -> [LeetCode](https://leetcode.com/problems/next-permutation/description/)
 
Medium

A permutation of an array of integers is an arrangement of its members into a sequence or linear order.

For example, for arr = [1,2,3], the following are all the permutations of arr: [1,2,3], [1,3,2], [2, 1, 3], [2, 3, 1], [3,1,2], [3,2,1].
The next permutation of an array of integers is the next lexicographically greater permutation of its integer. More formally, if all the permutations of the array are sorted in one container according to their lexicographical order, then the next permutation of that array is the permutation that follows it in the sorted container. If such arrangement is not possible, the array must be rearranged as the lowest possible order (i.e., sorted in ascending order).

For example, the next permutation of arr = [1,2,3] is [1,3,2].
Similarly, the next permutation of arr = [2,3,1] is [3,1,2].
While the next permutation of arr = [3,2,1] is [1,2,3] because [3,2,1] does not have a lexicographical larger rearrangement.
Given an array of integers nums, find the next permutation of nums.

The replacement must be in place and use only constant extra memory.

 

Example 1:

Input: nums = [1,2,3]
Output: [1,3,2]

Example 2:

Input: nums = [3,2,1]
Output: [1,2,3]

Example 3:

Input: nums = [1,1,5]
Output: [1,5,1]
 

Constraints:

1 <= nums.length <= 100
0 <= nums[i] <= 100

# Code
```cpp []
class Solution {
public:
    void nextPermutation(vector<int>& nums) {
        int n  = nums.size();
        int ind = -1;
        for(int i=n-2 ; i>=0 ; --i){
            if(nums[i] < nums[i+1]){
                ind = i;
                break;
            }
        }
        if(ind == -1){
            reverse(nums.begin() , nums.end());
            return;
        }
        for(int i=n-1 ; i>ind ; --i){
            if(nums[i] > nums[ind]){
                swap(nums[i] , nums[ind]);
                break;
            }
        }
        reverse(nums.begin() + ind + 1 , nums.end());
    }
};
```

---------------

## Array Leaders -> [GFG](https://www.geeksforgeeks.org/problems/leaders-in-an-array-1587115620/1)
Difficulty: Easy

You are given an array arr of positive integers. Your task is to find all the leaders in the array. An element is considered a leader if it is greater than or equal to all elements to its right. The rightmost element is always a leader.

Examples:

Input: arr = [16, 17, 4, 3, 5, 2]
Output: [17, 5, 2]
Explanation: Note that there is nothing greater on the right side of 17, 5 and, 2.


Input: arr = [10, 4, 2, 4, 1]
Output: [10, 4, 4, 1]
Explanation: Note that both of the 4s are in output, as to be a leader an equal element is also allowed on the right. side


Input: arr = [5, 10, 20, 40]
Output: [40]
Explanation: When an array is sorted in increasing order, only the rightmost element is leader.


Input: arr = [30, 10, 10, 5]
Output: [30, 10, 10, 5]
Explanation: When an array is sorted in non-increasing order, all elements are leaders.


Constraints:

1 <= arr.size() <= 106
0 <= arr[i] <= 106


Expected Complexities

Time Complexity: O(n)
Auxiliary Space: O(1)


Company Tags

PayuAdobe


Topic Tags

ArraysData Structures



# Code
```cpp []


class Solution {
    // Function to find the leaders in the array.
  public:
    vector<int> leaders(vector<int>& arr) {
        int n = arr.size();
        
        int maxi = arr[n-1];
        
        vector<int> ans;
        ans.push_back(maxi);
        
        for(int i=n-2 ; i>=0 ; --i){
            if(arr[i] >= maxi){ 
                ans.insert(ans.begin(),arr[i]);
                maxi = arr[i];
            }
        }
        
        return ans;
        
    }
};
```

---------------

# 128. Longest Consecutive Sequence -> [LeetCode](https://leetcode.com/problems/longest-consecutive-sequence/description/)
 
Medium
 
Given an unsorted array of integers nums, return the length of the longest consecutive elements sequence.

You must write an algorithm that runs in O(n) time.

 

Example 1:

Input: nums = [100,4,200,1,3,2]
Output: 4
Explanation: The longest consecutive elements sequence is [1, 2, 3, 4]. Therefore its length is 4.


Example 2:

Input: nums = [0,3,7,2,5,8,4,6,0,1]
Output: 9


Example 3:

Input: nums = [1,0,1,2]
Output: 3
 

Constraints:

0 <= nums.length <= 105
-109 <= nums[i] <= 109

# Code
```cpp []
class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        int n = nums.size();
        if(n == 0) return 0;
        int longest = 1;
        unordered_set<int> set1;
        for(const int i:nums) set1.insert(i);
        for(const int i:set1){
            if( set1.find(i - 1) == set1.end() ){
                int x = i;
                int cnt = 1;
                while( set1.find(x + 1) != set1.end() ){
                    cnt++;
                    x++;
                }
                longest = max(longest , cnt);
            }
        }
        return longest;
    }
};
```

------------


## Set Matrix Zeros -> [GFG](https://www.geeksforgeeks.org/problems/set-matrix-zeroes/1)

Difficulty: Medium 

You are given a 2D matrix mat[][] of size n x m. The task is to modify the matrix such that if mat[i][j] is 0, all the elements in the i-th row and j-th column are set to 0.

Examples:

Input: 
    ![image](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/898467/Web/Other/blobid1_1751352682.jpg)
Output: 
    ![image](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/898467/Web/Other/blobid3_1751352733.jpg)
    
Explanation: mat[1][1] = 0, so all elements in row 1 and column 1 are updated to zeroes.


Input: 
![image](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/874880/Web/Other/blobid0_1753182969.jpg)
    
Output: 
![image](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/874880/Web/Other/blobid1_1753183001.jpg)
    
Explanation: mat[0][0] and mat[0][3] are 0s, so all elements in row 0, column 0 and column 3 are updated to zeroes.


Constraints:

1 ≤ n, m ≤ 500
- 231 ≤ mat[i][j] ≤ 231 - 1


Expected Complexities

Time Complexity: O(n * m)
Auxiliary Space: O(1)


Company Tags

ExpediaAmazonYahooTCSService NowGoogleOracle


Topic Tags

GreedyMatrix



# Code
```cpp []
class Solution {
  public:
    void setMatrixZeroes(vector<vector<int>> &mat) {
        int n = mat.size() , m = mat[0].size() , col0 = 1 , row0 = 1;
        for(int i=0 ; i<n ; ++i){
            for(int j=0 ; j<m ; j++){
                if(mat[i][j] == 0){
                    mat[i][0] = 0;
                    if(j == 0) col0 = 0;
                    else mat[0][j] = 0;
                }
            }
        }
        
        for(int i=1 ; i<n ; ++i){
            for(int j=1 ; j<m ; j++){
                if(mat[i][j] != 0){
                    if(mat[i][0] == 0 || mat[0][j] == 0){
                        mat[i][j] = 0;
                    }
                }
            }
        }
        
        if(mat[0][0] == 0) for(int j=0 ; j<m ; ++j) mat[0][j] = 0;
        if(col0 == 0) for(int i=0 ; i<n ; ++i) mat[i][0] = 0;
        
    }
};
```

------------


# Binary Search

-----------
# Implement Lower Bound -> [GFG](https://www.geeksforgeeks.org/problems/implement-lower-bound/1)

Difficulty: Easy

Given a sorted array arr[] and a number target, the task is to find the lower bound of the target in this given array. The lower bound of a number is defined as the smallest index in the sorted array where the element is greater than or equal to the given number.

Note: If all the elements in the given array are smaller than the target, the lower bound will be the length of the array. 

Examples :

Input:  arr[] = [2, 3, 7, 10, 11, 11, 25], target = 9
Output: 3
Explanation: 3 is the smallest index in arr[] where element (arr[3] = 10) is greater than or equal to 9.


Input: arr[] = [2, 3, 7, 10, 11, 11, 25], target = 11
Output: 4
Explanation: 4 is the smallest index in arr[] where element (arr[4] = 11) is greater than or equal to 11.


Input: arr[] = [2, 3, 7, 10, 11, 11, 25], target = 100
Output: 7
Explanation: As no element in arr[] is greater than 100, return the length of array.


Constraints:

1 ≤ arr.size() ≤ 106
1 ≤ arr[i] ≤ 106
1 ≤ target ≤ 106


Expected Complexities

Time Complexity: O(log n)
Auxiliary Space: O(1)


Topic Tags

Binary SearchArraysAlgorithms


# code
```cpp []
class Solution {
  public:
    int lowerBound(vector<int>& arr, int target) {
        int l = 0 , r = arr.size() - 1;
        int ans = r + 1;
        while(l<=r){
            int mid = l + (r - l) / 2;
            if(arr[mid] >= target){ 
                ans = mid;
                r = mid - 1;
            }else l = mid + 1;
        }
        return ans;
    }
};
```


--------------------


# Implement Upper Bound -> [GFG](https://www.geeksforgeeks.org/problems/implement-upper-bound/1)

Difficulty: Easy

Given a sorted array arr[] and a number target, the task is to find the upper bound of the target in this given array.
The upper bound of a number is defined as the smallest index in the sorted array where the element is greater than the given number.

Note: If all the elements in the given array are smaller than or equal to the target, the upper bound will be the length of the array.

Examples :

Input: arr[] = [2, 3, 7, 10, 11, 11, 25], target = 9
Output: 3
Explanation: 3 is the smallest index in arr[], at which element (arr[3] = 10) is larger than 9.


Input: arr[] = [2, 3, 7, 10, 11, 11, 25], target = 11
Output: 6
Explanation: 6 is the smallest index in arr[], at which element (arr[6] = 25) is larger than 11.


Input: arr[] = [2, 3, 7, 10, 11, 11, 25], target = 100
Output: 7
Explanation: As no element in arr[] is greater than 100, return the length of array.


Constraints:

1 ≤ arr.size() ≤ 106
1 ≤ arr[i] ≤ 106
1 ≤ target ≤ 106


Expected Complexities

Time Complexity: O(log n)
Auxiliary Space: O(1)


Topic Tags

Binary SearchArraysAlgorithms

# code
```cpp []
class Solution {
  public:
    int upperBound(vector<int>& arr, int target) {
        int n = arr.size();
        int l = 0 , r = n - 1;
        int ans = n;
        while(l<=r){
            int mid = l + (r - l) / 2;
            if(arr[mid] > target){
                ans = mid;
                r = mid - 1;
            }else l = mid + 1;
        }
        return ans;
    }
};

```


--------------------

# Search insert position of K in a sorted array -> [GFG](https://www.geeksforgeeks.org/problems/search-insert-position-of-k-in-a-sorted-array/1)

Difficulty: Easy

Given a sorted array arr[] (0-index based) of distinct integers and an integer k, find the index of k if it is present in the arr[]. If not, return the index where k should be inserted to maintain the sorted order.

Examples :

Input: arr[] = [1, 3, 5, 6], k = 5
Output: 2
Explanation: Since 5 is found at index 2 as arr[2] = 5, the output is 2.


Input: arr[] = [1, 3, 5, 6], k = 2
Output: 1
Explanation: The element 2 is not present in the array, but inserting it at index 1 will maintain the sorted order.


Input: arr[] = [2, 6, 7, 10, 14], k = 15
Output: 5
Explanation: The element 15 is not present in the array, but inserting it after index 4 will maintain the sorted order.


Constraints:

1 ≤ arr.size() ≤ 104
-103 ≤ arr[i] ≤ 103
-103 ≤ k ≤ 103


Expected Complexities

Time Complexity: O(log n)
Auxiliary Space: O(1)


Company Tags

Microsoft


Topic Tags

SearchingAlgorithms


# code
```cpp []
class Solution {
  public:
    int searchInsertK(vector<int> &arr, int k) {
        // code here
        int n = arr.size() , ans = n , l = 0 , h = n - 1;
        
        while(l<=h){
            int mid = l + (h -l)/2;
            if(arr[mid] >= k){
                ans = mid;
                h = mid - 1;
            }else l = mid + 1;
        }
        
        return ans;
        
    }
};
```


--------------------

# Floor in a Sorted Array -> [GFG](https://www.geeksforgeeks.org/problems/floor-in-a-sorted-array-1587115620/1)

Difficulty: Easy

Given a sorted array arr[] and an integer x, find the index (0-based) of the largest element in arr[] that is less than or equal to x. This element is called the floor of x. If such an element does not exist, return -1.

Note: In case of multiple occurrences of ceil of x, return the index of the last occurrence.

Examples

Input: arr[] = [1, 2, 8, 10, 10, 12, 19], x = 5
Output: 1
Explanation: Largest number less than or equal to 5 is 2, whose index is 1.

Input: arr[] = [1, 2, 8, 10, 10, 12, 19], x = 11
Output: 4
Explanation: Largest Number less than or equal to 11 is 10, whose indices are 3 and 4. The index of last occurrence is 4.

Input: arr[] = [1, 2, 8, 10, 10, 12, 19], x = 0
Output: -1
Explanation: No element less than or equal to 0 is found. So, output is -1.


Constraints:

1 ≤ arr.size() ≤ 106
1 ≤ arr[i] ≤ 106
0 ≤ x ≤ arr[n-1]


Expected Complexities

Time Complexity: O(log n)
Auxiliary Space: O(1)


Company Tags

Amazon


Topic Tags

SearchingSortingAlgorithms


# code
```cpp []
class Solution {
  public:
    int findFloor(vector<int>& arr, int x) {
        int n = arr.size() , ans = -1 , l = 0 , h = n - 1;
        while(l<=h){
            int mid = l + (h - l) / 2;
            if(arr[mid] <= x){
                ans = mid;
                l = mid + 1;
            }else{
                h = mid - 1;
            }
        }
        return ans;
    }
};

```


--------------------


# 34. Find First and Last Position of Element in Sorted Array -> [LeetCode](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/description/)
 
Medium
 
Given an array of integers nums sorted in non-decreasing order, find the starting and ending position of a given target value.

If target is not found in the array, return [-1, -1].

You must write an algorithm with O(log n) runtime complexity.

 

Example 1:

Input: nums = [5,7,7,8,8,10], target = 8
Output: [3,4]


Example 2:

Input: nums = [5,7,7,8,8,10], target = 6
Output: [-1,-1]


Example 3:

Input: nums = [], target = 0
Output: [-1,-1]
 

Constraints:

0 <= nums.length <= 105
-109 <= nums[i] <= 109
nums is a non-decreasing array.
-109 <= target <= 109

# Code
```cpp []
class Solution {
    int firstOcu(vector<int> &arr , int n , int x){
       int ans = -1;
       int l = 0 , r = n - 1;
       while(l<=r){
           int mid = (l + r )/2;
           if(arr[mid] == x){
               ans = mid;
               r = mid - 1;
           }else if(arr[mid] < x) l = mid + 1;
           else r = mid - 1;
       }
       return ans;
    }
    
    int lastOcu(vector<int> &arr , int n , int x){
       int ans = -1;
       int l = 0 , r = n - 1;
       while(l<=r){
           int mid = (l + r )/2;
           if(arr[mid] == x){
               ans = mid;
               l = mid + 1;
           }else if(arr[mid] < x) l = mid + 1;
           else r = mid - 1;
       }
       return ans;
    }
    
public:
    vector<int> searchRange(vector<int>& nums, int target) {
        int n = nums.size();
        int first = firstOcu(nums,n,target);
        if(first == -1) return {-1,-1};
        int last = lastOcu(nums,n,target);
        return {first, last};
    }
};
```

-----------------


# 81. Search in Rotated Sorted Array II -> [LeetCode](https://leetcode.com/problems/search-in-rotated-sorted-array-ii/description/)
 
Medium
 
There is an integer array nums sorted in non-decreasing order (not necessarily with distinct values).

Before being passed to your function, nums is rotated at an unknown pivot index k (0 <= k < nums.length) such that the resulting array is [nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]] (0-indexed). For example, [0,1,2,4,4,4,5,6,6,7] might be rotated at pivot index 5 and become [4,5,6,6,7,0,1,2,4,4].

Given the array nums after the rotation and an integer target, return true if target is in nums, or false if it is not in nums.

You must decrease the overall operation steps as much as possible.

 

Example 1:

Input: nums = [2,5,6,0,0,1,2], target = 0
Output: true


Example 2:

Input: nums = [2,5,6,0,0,1,2], target = 3
Output: false
 

Constraints:

1 <= nums.length <= 5000
-104 <= nums[i] <= 104
nums is guaranteed to be rotated at some pivot.
-104 <= target <= 104

# Code
```cpp []
class Solution {
public:
    bool search(vector<int>& nums, int target) {
        int n = nums.size();
        int l = 0 , h = n - 1;
        while(l<=h){
            int mid = (l + h)/2;
            if(nums[mid] == target) return true;
            if(nums[l] == nums[mid] && nums[mid] == nums[h]){
                l++;
                h--;
                continue;
            }
            if(nums[l] <= nums[mid]){
                if(nums[l] <= target && nums[mid] >= target ) h = mid - 1;
                else l = mid + 1;
            }
            else{
                if(nums[mid] <= target && nums[h] >= target ) l = mid + 1;
                else h = mid - 1;
            }
        }
        return false;
    }
};
```


-------------

# Find Kth Rotation -> [GFG](https://www.geeksforgeeks.org/problems/rotation4723/1)

Difficulty: Easy

Given an increasing sorted rotated array arr[] of distinct integers. The array is right-rotated k times. Find the value of k.
Let's suppose we have an array arr[] = [2, 4, 6, 9], if we rotate it by 2 times it will look like this:
After 1st Rotation : [9, 2, 4, 6]
After 2nd Rotation : [6, 9, 2, 4]

Examples:

Input: arr[] = [5, 1, 2, 3, 4]
Output: 1
Explanation: The given array is [5, 1, 2, 3, 4]. The original sorted array is [1, 2, 3, 4, 5]. We can see that the array was rotated 1 times to the right.


Input: arr = [1, 2, 3, 4, 5]
Output: 0
Explanation: The given array is not rotated.


Constraints:

1 ≤ arr.size() ≤105
1 ≤ arr[i] ≤ 107


Expected Complexities

Time Complexity: O(log n)
Auxiliary Space: O(1)


Company Tags

FlipkartAmazonABCO


Topic Tags

ArraysSearchingData StructuresAlgorithms


# Code
```cpp []
class Solution {
  public:
    int findKRotation(vector<int> &arr) {
        int n = arr.size() , l = 0 , h = n - 1;
        int low = INT_MAX, index = -1;
        
        while(l<=h){
            int mid = l + (h-l)/2;
            
            if(arr[l] <= arr[h]){
                if(arr[l] < low){
                    low = arr[l];
                    index = l;
                }
                break;
            }
            
            if(arr[l] <= arr[mid]){
                if(arr[l] < low){
                    low = arr[l];
                    index = l;
                }
                l = mid + 1;
            }
            else{
                if(arr[mid] < low){
                    low = arr[mid];
                    index = mid;
                }
                h = mid - 1;
            }
            
        }
        
        return index;
    }
};

```


-------------


# 540. Single Element in a Sorted Array -> [LeetCode](https://leetcode.com/problems/single-element-in-a-sorted-array/description/)
 
Medium
 
You are given a sorted array consisting of only integers where every element appears exactly twice, except for one element which appears exactly once.

Return the single element that appears only once.

Your solution must run in O(log n) time and O(1) space.

 

Example 1:

Input: nums = [1,1,2,3,3,4,4,8,8]
Output: 2


Example 2:

Input: nums = [3,3,7,7,10,11,11]
Output: 10
 

Constraints:

1 <= nums.length <= 105
0 <= nums[i] <= 105

# Code
```cpp []
class Solution {
public:
    int singleNonDuplicate(vector<int>& nums) {
        int n = nums.size();

        if(n==1) return nums[0];

        if(nums[0] != nums[1]) return nums[0];
        if(nums[n-1] != nums[n-2]) return nums[n-1];

        int l = 1 , h = n-2;
        while(l<=h){
            int mid =  l + (h-l) / 2;
            if(nums[mid - 1] != nums[mid] && nums[mid] != nums[mid + 1]) return nums[mid];
            if((mid % 2 == 1 && nums[mid] == nums[mid-1]) || 
               (mid % 2 == 0 && nums[mid] == nums[mid + 1]) ) l = mid + 1;
            else h = mid - 1;
        }
        return -1;
    }
};
```


---------



# 162. Find Peak Element -> [LeetCode](https://leetcode.com/problems/find-peak-element/description/)
 
Medium
 
A peak element is an element that is strictly greater than its neighbors.

Given a 0-indexed integer array nums, find a peak element, and return its index. If the array contains multiple peaks, return the index to any of the peaks.

You may imagine that nums[-1] = nums[n] = -∞. In other words, an element is always considered to be strictly greater than a neighbor that is outside the array.

You must write an algorithm that runs in O(log n) time.

 

Example 1:

Input: nums = [1,2,3,1]
Output: 2
Explanation: 3 is a peak element and your function should return the index number 2.


Example 2:

Input: nums = [1,2,1,3,5,6,4]
Output: 5
Explanation: Your function can return either index number 1 where the peak element is 2, or index number 5 where the peak element is 6.
 

Constraints:

1 <= nums.length <= 1000
-231 <= nums[i] <= 231 - 1
nums[i] != nums[i + 1] for all valid i.


# Code
```cpp []
class Solution {
public:
    int findPeakElement(vector<int>& nums) {
        int n = nums.size();
        if(n == 1) return 0;
        if(nums[0] > nums[1]) return 0;
        if(nums[n-1] > nums[n-2]) return n-1;
        int l = 1 , h = n-2;
        while(l<=h){
            int mid = l + (h-l)/2;
            if(nums[mid - 1] < nums[mid] && nums[mid] > nums[mid + 1]) return mid;
            if(nums[mid - 1] < nums[mid]) l = mid + 1;
            else h = mid - 1;
        }
        return -1;
    }
};
```

------------------------


# 69. Sqrt(x) -> [LeetCode](https://leetcode.com/problems/sqrtx/description/)
 
Easy

Given a non-negative integer x, return the square root of x rounded down to the nearest integer. The returned integer should be non-negative as well.

You must not use any built-in exponent function or operator.

For example, do not use pow(x, 0.5) in c++ or x ** 0.5 in python.
 

Example 1:

Input: x = 4
Output: 2
Explanation: The square root of 4 is 2, so we return 2.


Example 2:

Input: x = 8
Output: 2
Explanation: The square root of 8 is 2.82842..., and since we round it down to the nearest integer, 2 is returned.
 

Constraints:

0 <= x <= 231 - 1

# Code
```cpp []
class Solution {
public:
    int mySqrt(int x) {
        int l = 0 , h = x , ans = 0;
        while(l<=h){
            long long mid = (l + h)/2;
            if(mid*mid <= x) l = mid + 1 , ans = mid;
            else h = mid - 1;
        }
        return ans;
    }
};
```

---------------


# Find nth root of m -> [GFG](https://www.geeksforgeeks.org/problems/find-nth-root-of-m5843/1)

Difficulty: Medium

You are given 2 numbers n and m, the task is to find n√m (nth root of m). If the root is not integer then returns -1.

Examples :

Input: n = 3, m = 27
Output: 3
Explanation: 33 = 27

Input: n = 3, m = 9
Output: -1
Explanation: 3rd root of 9 is not integer.

Input: n = 4, m = 625
Output: 5
Explanation: 54 = 625


Constraints:

1 ≤ n ≤ 30
0 ≤ m ≤ 109


Expected Complexities

Time Complexity: O(n log m)
Auxiliary Space: O(1)


Company Tags

DirectiAccenture


Topic Tags

MathematicalAlgorithmsBinary Search


# Code
```cpp []
class Solution {
    int findRoot(int b,int expo,int m){
        long long ans = 1, base = b;
        while(expo>0){
            if(expo % 2){
                expo--;
                ans = ans * base;
            }else{
                expo/=2;
                base *= base;
            }
            if(ans > m) return 2;
        }
        if(ans == m) return 1;
        return 0;
    }
    
  public:
    int nthRoot(int n, int m) {
        int l = 1 , h = m;
        while(l<=h){
            int mid = l + (h-l)/2;
            int res = findRoot(mid,n ,m);
            if(res == 1) return mid;
            else if(res == 2) h = mid - 1;
            else l = mid + 1;
        }
        return -1;
    }
};
```

---------------



# 1482. Minimum Number of Days to Make m Bouquets -> [LeetCode](https://leetcode.com/problems/minimum-number-of-days-to-make-m-bouquets/description/)
 
Medium
 
You are given an integer array bloomDay, an integer m and an integer k.

You want to make m bouquets. To make a bouquet, you need to use k adjacent flowers from the garden.

The garden consists of n flowers, the ith flower will bloom in the bloomDay[i] and then can be used in exactly one bouquet.

Return the minimum number of days you need to wait to be able to make m bouquets from the garden. If it is impossible to make m bouquets return -1.

 

Example 1:

Input: bloomDay = [1,10,3,10,2], m = 3, k = 1
Output: 3
Explanation: Let us see what happened in the first three days. x means flower bloomed and _ means flower did not bloom in the garden.
We need 3 bouquets each should contain 1 flower.
After day 1: [x, _, _, _, _]   // we can only make one bouquet.
After day 2: [x, _, _, _, x]   // we can only make two bouquets.
After day 3: [x, _, x, _, x]   // we can make 3 bouquets. The answer is 3.


Example 2:

Input: bloomDay = [1,10,3,10,2], m = 3, k = 2
Output: -1
Explanation: We need 3 bouquets each has 2 flowers, that means we need 6 flowers. We only have 5 flowers so it is impossible to get the needed bouquets and we return -1.


Example 3:

Input: bloomDay = [7,7,7,7,12,7,7], m = 2, k = 3
Output: 12
Explanation: We need 2 bouquets each should have 3 flowers.
Here is the garden after the 7 and 12 days:
After day 7: [x, x, x, x, _, x, x]
We can make one bouquet of the first three flowers that bloomed. We cannot make another bouquet from the last three flowers that bloomed because they are not adjacent.
After day 12: [x, x, x, x, x, x, x]
It is obvious that we can make two bouquets in different ways.
 

Constraints:

bloomDay.length == n
1 <= n <= 105
1 <= bloomDay[i] <= 109
1 <= m <= 106
1 <= k <= n

# Code
```cpp []
class Solution {
    bool isPossible(vector<int>& arr, int day , int m , int k){
        int cnt = 0 , noOfB = 0;
        for(int i=0 ; i<arr.size() ; ++i){
            if(day >= arr[i]) cnt++;
            else{
                noOfB += (cnt/k);
                cnt = 0;
            }
        }
        noOfB += (cnt/k);
        return noOfB >= m;
    }

public:
    int minDays(vector<int>& bloomDay, int m, int k) {
        long long val = (m * 1ll ) * (k * 1ll);
        int n = bloomDay.size();
        if(val > n) return -1;
        int mini = INT_MAX , maxi = INT_MIN;
        for(const int i:bloomDay) mini = min(mini,i), maxi = max(maxi,i);

        int low = mini , high = maxi;
        while(low<=high){
            int mid = low + (high-low)/2;
            if(isPossible(bloomDay, mid , m , k)) high = mid - 1;
            else low = mid + 1;
        }
        return low;
    }
};
```

----------------



# 875. Koko Eating Bananas -> [LeetCode](https://leetcode.com/problems/koko-eating-bananas/description/)
 
Medium


Koko loves to eat bananas. There are n piles of bananas, the ith pile has piles[i] bananas. The guards have gone and will come back in h hours.

Koko can decide her bananas-per-hour eating speed of k. Each hour, she chooses some pile of bananas and eats k bananas from that pile. If the pile has less than k bananas, she eats all of them instead and will not eat any more bananas during this hour.

Koko likes to eat slowly but still wants to finish eating all the bananas before the guards return.

Return the minimum integer k such that she can eat all the bananas within h hours.

 

Example 1:

Input: piles = [3,6,7,11], h = 8
Output: 4

Example 2:

Input: piles = [30,11,23,4,20], h = 5
Output: 30


Example 3:

Input: piles = [30,11,23,4,20], h = 6
Output: 23
 

Constraints:

1 <= piles.length <= 104
piles.length <= h <= 109
1 <= piles[i] <= 109

# Code
```cpp []
class Solution {
    int totalHour(vector<int>& arr, int hr,int n, int x){
        int ans = 0;
        for(int i=0 ; i<n ; ++i){
             ans += ceil( ( (double)(arr[i]) / (double)(hr) ) );
            if(ans > x) break;
        }
        return ans;
    }
public:
    int minEatingSpeed(vector<int> arr, int x) {
        sort(arr.begin() , arr.end());
        int n = arr.size() , l = 1 , h = arr[n-1];
        while(l<=h){
            int mid = l + (h-l)/2;
            if(totalHour(arr,mid,n,x) <= x) h = mid - 1;
            else l = mid + 1;
        }
        return l;
    }
};
```

-------------------


# 1539. Kth Missing Positive Number -> [LeetCode](https://leetcode.com/problems/kth-missing-positive-number/description/)
 
Easy
 
Given an array arr of positive integers sorted in a strictly increasing order, and an integer k.

Return the kth positive integer that is missing from this array.

 

Example 1:

Input: arr = [2,3,4,7,11], k = 5
Output: 9
Explanation: The missing positive integers are [1,5,6,8,9,10,12,13,...]. The 5th missing positive integer is 9.


Example 2:

Input: arr = [1,2,3,4], k = 2
Output: 6
Explanation: The missing positive integers are [5,6,7,...]. The 2nd missing positive integer is 6.
 

Constraints:

1 <= arr.length <= 1000
1 <= arr[i] <= 1000
1 <= k <= 1000
arr[i] < arr[j] for 1 <= i < j <= arr.length
 

Follow up:

Could you solve this problem in less than O(n) complexity?

# Code
```cpp []
class Solution {
public:
    int findKthPositive(vector<int>& arr, int k) {
        int n = arr.size(), low = 0 , high = n - 1;
        while(low<=high){
            int mid = low + (high - low)/2;
            int missing = arr[mid] - (mid+1);
            if(missing < k) low = mid + 1;
            else high = mid - 1;
        }
        return (high + 1 + k);
    }
};
```

---------------------







