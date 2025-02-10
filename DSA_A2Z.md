# DSA

## GeeksForGeeks

#Count Digits
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

## leetcode
# 7. Reverse Integer

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
