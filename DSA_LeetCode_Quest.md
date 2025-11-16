---------------------------------------------------------------------------------------
#  DSA Leetcode Quest - [Link](https://leetcode.com/quest/data-structures-and-algorithms-quest/)
---------------------------------------------------------------------------------------

# Q1.[ Concatenation of Array](https://leetcode.com/problems/concatenation-of-array/description)
 
Easy
 
Given an integer array nums of length n, you want to create an array ans of length 2n where ans[i] == nums[i] and ans[i + n] == nums[i] for 0 <= i < n (0-indexed).

Specifically, ans is the concatenation of two nums arrays.

Return the array ans.

 

Example 1:

Input: nums = [1,2,1]

Output: [1,2,1,1,2,1]

Explanation: The array ans is formed as follows:
- ans = [nums[0],nums[1],nums[2],nums[0],nums[1],nums[2]]
- ans = [1,2,1,1,2,1]


Example 2:

Input: nums = [1,3,2,1]

Output: [1,3,2,1,1,3,2,1]

Explanation: The array ans is formed as follows:
- ans = [nums[0],nums[1],nums[2],nums[3],nums[0],nums[1],nums[2],nums[3]]
- ans = [1,3,2,1,1,3,2,1]
 

Constraints:

n == nums.length
1 <= n <= 1000
1 <= nums[i] <= 1000

# Code
```cpp []
class Solution {
public:
    vector<int> getConcatenation(vector<int>& nums) {
        vector<int> res(nums.begin() , nums.end());
        for(int num:nums) res.push_back(num);
        return res;
    }
};
```

-----------------------------------------------------------------------------

# Q2. [Shuffle the Array](https://leetcode.com/problems/shuffle-the-array/description/)
 
Easy
 
Given the array nums consisting of 2n elements in the form [x1,x2,...,xn,y1,y2,...,yn].

Return the array in the form [x1,y1,x2,y2,...,xn,yn].

 

Example 1:

Input: nums = [2,5,1,3,4,7], n = 3

Output: [2,3,5,4,1,7] 

Explanation: Since x1=2, x2=5, x3=1, y1=3, y2=4, y3=7 then the answer is [2,3,5,4,1,7].


Example 2:

Input: nums = [1,2,3,4,4,3,2,1], n = 4

Output: [1,4,2,3,3,2,4,1]


Example 3:

Input: nums = [1,1,2,2], n = 2

Output: [1,2,1,2]
 

Constraints:

1 <= n <= 500
nums.length == 2n
1 <= nums[i] <= 10^3


# Code
```cpp []
class Solution {
public:
    vector<int> shuffle(vector<int>& nums, int n) {
        vector<int> res;
        int l = 0 , r = n;

        while(l<n && r<n*2){
            res.push_back(nums[l++]);
            res.push_back(nums[r++]);
        }

        return res;
    }
};
```

-------------------------------------------------------------------------------------------





