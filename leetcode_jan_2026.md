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



