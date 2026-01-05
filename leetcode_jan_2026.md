-----------------------------------------------------------
# LeetCode problems for JANUARY - 2026
-----------------------------------------------------------


# 66. Plus One -> [LeetCode](https://leetcode.com/problems/plus-one)

Easy

You are given a large integer represented as an integer array digits, where each digits[i] is the ith digit of the integer. The digits are ordered from most significant to least significant in left-to-right order. The large integer does not contain any leading 0's.

Increment the large integer by one and return the resulting array of digits.

 

Example 1:

Input: digits = [1,2,3]

Output: [1,2,4]

Explanation: The array represents the integer 123.
Incrementing by one gives 123 + 1 = 124.
Thus, the result should be [1,2,4].



Example 2:

Input: digits = [4,3,2,1]

Output: [4,3,2,2]

Explanation: The array represents the integer 4321.
Incrementing by one gives 4321 + 1 = 4322.
Thus, the result should be [4,3,2,2].


Example 3:

Input: digits = [9]

Output: [1,0]

Explanation: The array represents the integer 9.
Incrementing by one gives 9 + 1 = 10.
Thus, the result should be [1,0].
 


Constraints:

1 <= digits.length <= 100
0 <= digits[i] <= 9
digits does not contain any leading 0's.



# Code
```cpp []
class Solution {
 public:
  vector<int> plusOne(vector<int>& nums) {

    int n = nums.size();

    for(int i=n-1 ; i>=0 ; --i){
        if(nums[i] < 9){
            ++nums[i];
            return nums;
        }
        nums[i] = 0;
    }

    nums.insert(nums.begin() , 1);
    return nums;
  }
};
```

----------------------------------------------------------------------------------------


# 961. N-Repeated Element in Size 2N Array -> [LeetCode](https://leetcode.com/problems/n-repeated-element-in-size-2n-array/description/)

Easy

You are given an integer array nums with the following properties:

nums.length == 2 * n.
nums contains n + 1 unique elements.
Exactly one element of nums is repeated n times.
Return the element that is repeated n times.

 

Example 1:

Input: nums = [1,2,3,3]

Output: 3




Example 2:

Input: nums = [2,1,2,5,3,2]

Output: 2




Example 3:

Input: nums = [5,1,5,2,5,3,5,4]

Output: 5
 

Constraints:

2 <= n <= 5000
nums.length == 2 * n
0 <= nums[i] <= 104
nums contains n + 1 unique elements and one of them is repeated exactly n times.



# Code
```cpp []
class Solution {
public:
    int repeatedNTimes(vector<int>& A) {
        for (int i = 0; i < A.size() - 2; ++i)
            if (A[i] == A[i + 1] || A[i] == A[i + 2])
                return A[i];
        return A.back();
    }
};

```

-----------------------------------------------------------------------------------------------------------------------------------



# [1411. Number of Ways to Paint N × 3 Grid](https://leetcode.com/problems/number-of-ways-to-paint-n-3-grid/)

Hard

You have a grid of size n x 3 and you want to paint each cell of the grid with exactly one of the three colors: Red, Yellow, or Green while making sure that no two adjacent cells have the same color (i.e., no two cells that share vertical or horizontal sides have the same color).

Given n the number of rows of the grid, return the number of ways you can paint this grid. As the answer may grow large, the answer must be computed modulo 109 + 7.


Example 1:

![img](https://assets.leetcode.com/uploads/2020/03/26/e1.png)

Input: n = 1

Output: 12

Explanation: There are 12 possible way to paint the grid as shown.



Example 2:

Input: n = 5000

Output: 30228214
 

Constraints:

n == grid.length
1 <= n <= 5000



# Code
```cpp []
class Solution {
public:
    int numOfWays(int n) {
        const int MOD = 1000000007;
        long long x = 6, y = 6;

        for (int i = 2; i <= n; i++) {
            long long new_x = (3 * x + 2 * y) % MOD;
            long long new_y = (2 * x + 2 * y) % MOD;
            x = new_x;
            y = new_y;
        }

        return (x + y) % MOD;
    }
};
```

-----------------------------------------------------------------------------------------------------------


# [1390. Four Divisors](https://leetcode.com/problems/four-divisors/)

Medium
 
Given an integer array nums, return the sum of divisors of the integers in that array that have exactly four divisors. If there is no such integer in the array, return 0.

 

Example 1:

Input: nums = [21,4,7]

Output: 32

Explanation: 

21 has 4 divisors: 1, 3, 7, 21
4 has 3 divisors: 1, 2, 4
7 has 2 divisors: 1, 7
The answer is the sum of divisors of 21 only.



Example 2:

Input: nums = [21,21]

Output: 64



Example 3:

Input: nums = [1,2,3,4,5]

Output: 0
 

Constraints:

1 <= nums.length <= 104
1 <= nums[i] <= 105



# Code
```cpp []
class Solution {
public:
    int sumFourDivisors(vector<int>& nums) {
        int res = 0;
        for (int n : nums) {
            int val = sumOne(n);
            if (val != -1) res += val;
        }
        return res;
    }

    int sumOne(int n) {
        int p = round(cbrt(n));
        if ((long long)p * p * p == n && isPrime(p)) {
            return 1 + p + p*p + p*p*p;
        }

        for (int i = 2; i * i <= n; i++) {
            if (n % i == 0) {
                int a = i, b = n / i;
                if (a != b && isPrime(a) && isPrime(b)) {
                    return 1 + a + b + n;
                }
                return -1;
            }
        }
        return -1;
    }

    bool isPrime(int x) {
        if (x < 2) return false;
        for (int i = 2; i * i <= x; i++) {
            if (x % i == 0) return false;
        }
        return true;
    }
};
```

-----------------------------------------------------------------------------------------------------------------------


# 1975. Maximum Matrix Sum

Medium
 
You are given an n x n integer matrix. You can do the following operation any number of times:

Choose any two adjacent elements of matrix and multiply each of them by -1.
Two elements are considered adjacent if and only if they share a border.

Your goal is to maximize the summation of the matrix's elements. Return the maximum sum of the matrix's elements using the operation mentioned above.

 

Example 1:


Input: matrix = [[1,-1],[-1,1]]

Output: 4

Explanation: We can follow the following steps to reach sum equals 4:
- Multiply the 2 elements in the first row by -1.
- Multiply the 2 elements in the first column by -1.



Example 2:


Input: matrix = [[1,2,3],[-1,-2,-3],[1,2,3]]

Output: 16

Explanation: We can follow the following step to reach sum equals 16:

- Multiply the 2 last elements in the second row by -1.
 

Constraints:

n == matrix.length == matrix[i].length
2 <= n <= 250
-105 <= matrix[i][j] <= 105



