---------------------------------------------------------------------------------------
#  DSA Leetcode Quest - [Link](https://leetcode.com/quest/data-structures-and-algorithms-quest/)
---------------------------------------------------------------------------------------

# Array I
---
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

# Q3.[ Max Consecutive Ones](https://leetcode.com/problems/max-consecutive-ones/description)
 
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
        int res = 0 , cnt = 0;   
        for(const int num:nums){
            if(num == 1) cnt++;
            else cnt = 0;
            res = max(res , cnt);
        }
        return res;
    }
};
```

-----------------------------------------------------------------------------------------------------------
-----------------------------------------------------------------------------------------------------------

# Array II
---


# IQ1. [Set Mismatch](https://leetcode.com/problems/set-mismatch/description)

Easy
 
You have a set of integers s, which originally contains all the numbers from 1 to n. Unfortunately, due to some error, one of the numbers in s got duplicated to another number in the set, which results in repetition of one number and loss of another number.

You are given an integer array nums representing the data status of this set after the error.

Find the number that occurs twice and the number that is missing and return them in the form of an array.

 

Example 1:

Input: nums = [1,2,2,4]

Output: [2,3]


Example 2:

Input: nums = [1,1]

Output: [1,2]
 

Constraints:

2 <= nums.length <= 104
1 <= nums[i] <= 104

# Code
```cpp []
class Solution {
public:
    vector<int> findErrorNums(vector<int>& nums) {

        int n = nums.size();
        vector<int> res;

        int sum = 0;
        unordered_map<int,int> mpp;

        for(const int num:nums){
            mpp[num]++;
        }

        for(auto it:mpp){
            if(it.second > 1) res.push_back(it.first);
            sum += it.first;
        }

        int mis = ((n+1) * n)/2 - sum;
        res.push_back(mis);

        return res;
    }
};
```

-------------------------------------------------------------------------------


# Q2. [How Many Numbers Are Smaller Than the Current Number](https://leetcode.com/problems/how-many-numbers-are-smaller-than-the-current-number/description)
Easy
 
Given the array nums, for each nums[i] find out how many numbers in the array are smaller than it. That is, for each nums[i] you have to count the number of valid j's such that j != i and nums[j] < nums[i].

Return the answer in an array.

 

Example 1:

Input: nums = [8,1,2,2,3]

Output: [4,0,1,1,3]

Explanation: 
For nums[0]=8 there exist four smaller numbers than it (1, 2, 2 and 3). 
For nums[1]=1 does not exist any smaller number than it.
For nums[2]=2 there exist one smaller number than it (1). 
For nums[3]=2 there exist one smaller number than it (1). 
For nums[4]=3 there exist three smaller numbers than it (1, 2 and 2).


Example 2:

Input: nums = [6,5,4,8]

Output: [2,1,0,3]



Example 3:

Input: nums = [7,7,7,7]

Output: [0,0,0,0]
 

Constraints:

2 <= nums.length <= 500
0 <= nums[i] <= 100

# Code
```cpp []
class Solution {
public:
    vector<int> smallerNumbersThanCurrent(vector<int>& nums) {
        vector<int> res;

        vector<int> freq(101 , 0);
        for(const int num:nums) freq[num]++;

        vector<int> prefix(101 , 0);
        for(int i=1 ; i<101 ; ++i) prefix[i] = prefix[i-1] + freq[i-1];

        for(const int num:nums) res.push_back(prefix[num]);

        return res;
    }
};
```

------------------------------------------------------------------------------------------------------------------------


# IQ3. [Find All Numbers Disappeared in an Array](https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array)
 
Easy
 
Given an array nums of n integers where nums[i] is in the range [1, n], return an array of all the integers in the range [1, n] that do not appear in nums.

 

Example 1:

Input: nums = [4,3,2,7,8,2,3,1]

Output: [5,6]


Example 2:

Input: nums = [1,1]

Output: [2]
 

Constraints:

n == nums.length
1 <= n <= 105
1 <= nums[i] <= n
 

Follow up: Could you do it without extra space and in O(n) runtime? You may assume the returned list does not count as extra space.


# Code
```cpp []
class Solution {
public:
    vector<int> findDisappearedNumbers(vector<int>& nums) {
        
        int n = nums.size();

        for(int i=0 ; i<n ; ++i){
            int idx = abs(nums[i]) - 1;
            nums[idx] = -abs(nums[idx]);
        }

        vector<int> res;

        for(int i=0 ; i<n ; ++i){
           if(nums[i] > 0) res.push_back(i+1);
        }

        return res;
    }
};
```

-------------------------------------------------------------------------------------------------------------
-------------------------------------------------------------------------------------------------------------


# Stack

-------------------------------------------------------------------------------------------------------------

# Q1. [Build an Array With Stack Operations](https://leetcode.com/problems/build-an-array-with-stack-operations/description)
 
Medium
 
You are given an integer array target and an integer n.

You have an empty stack with the two following operations:

"Push": pushes an integer to the top of the stack.
"Pop": removes the integer on the top of the stack.
You also have a stream of the integers in the range [1, n].

Use the two stack operations to make the numbers in the stack (from the bottom to the top) equal to target. You should follow the following rules:

If the stream of the integers is not empty, pick the next integer from the stream and push it to the top of the stack.
If the stack is not empty, pop the integer at the top of the stack.
If, at any moment, the elements in the stack (from the bottom to the top) are equal to target, do not read new integers from the stream and do not do more operations on the stack.
Return the stack operations needed to build target following the mentioned rules. If there are multiple valid answers, return any of them.

 

Example 1:

Input: target = [1,3], n = 3

Output: ["Push","Push","Pop","Push"]

Explanation: Initially the stack s is empty. The last element is the top of the stack.
Read 1 from the stream and push it to the stack. s = [1].
Read 2 from the stream and push it to the stack. s = [1,2].
Pop the integer on the top of the stack. s = [1].
Read 3 from the stream and push it to the stack. s = [1,3].


Example 2:

Input: target = [1,2,3], n = 3

Output: ["Push","Push","Push"]

Explanation: Initially the stack s is empty. The last element is the top of the stack.
Read 1 from the stream and push it to the stack. s = [1].
Read 2 from the stream and push it to the stack. s = [1,2].
Read 3 from the stream and push it to the stack. s = [1,2,3].
Example 3:

Input: target = [1,2], n = 4

Output: ["Push","Push"]

Explanation: Initially the stack s is empty. The last element is the 
top of the stack.
Read 1 from the stream and push it to the stack. s = [1].
Read 2 from the stream and push it to the stack. s = [1,2].
Since the stack (from the bottom to the top) is equal to target, we stop the stack operations.
The answers that read integer 3 from the stream are not accepted.
 

Constraints:

1 <= target.length <= 100
1 <= n <= 100
1 <= target[i] <= n
target is strictly increasing.


# Code
```cpp []
class Solution {
public:
    vector<string> buildArray(vector<int>& target, int n) {
        vector<string> ops;
        int j=0;
        for(int i=1 ; j < target.size() && i<=n ; ++i){
            ops.push_back("Push");
            if( i == target[j]) j++;
            else ops.push_back("Pop");
        }

        return ops;
    }
};
```


---------------------------------------------------------



