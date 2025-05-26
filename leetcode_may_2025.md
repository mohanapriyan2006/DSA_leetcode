----
# LeetCode May - 2025
-----


# I121. Best Time to Buy and Sell Stock

Easy

You are given an array prices where prices[i] is the price of a given stock on the ith day.

You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock.

Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.

 

### Example 1:

Input: prices = [7,1,5,3,6,4] <br/>
Output: 5 <br/>
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.


### Example 2:

Input: prices = [7,6,4,3,1] <br/>
Output: 0 <br/>
Explanation: In this case, no transactions are done and the max profit = 0.
 

Constraints:

1 <= prices.length <= 105
0 <= prices[i] <= 104

# Code
```cpp []
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int maxP = 0;
        int mini = prices[0];

        for(int i=1 ; i<prices.size() ; ++i){
            int curP = prices[i] - mini;
            maxP = max(maxP,curP);
            mini = min(mini,prices[i]);
        }

        return maxP;
    }
};
```
------

# 217. Contains Duplicate

Easy

Given an integer array nums, return true if any value appears at least twice in the array, and return false if every element is distinct.

 

#### Example 1:

Input: nums = [1,2,3,1] <br/>

Output: true <br/>

Explanation: <br/>

The element 1 occurs at the indices 0 and 3.


#### Example 2:

Input: nums = [1,2,3,4] <br/>

Output: false <br/>

Explanation: <br/>

All elements are distinct.

#### Example 3:

Input: nums = [1,1,1,3,3,4,3,2,4,2] <br/>

Output: true <br/>
 
Constraints:

1 <= nums.length <= 105
-109 <= nums[i] <= 109

# Code
```cpp []
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        unordered_set<int> num;

        for(int i=0 ; i<nums.size() ; ++i){
            num.insert(nums[i]);
        }

        if( num.size() != nums.size()) return true;

        return false;
    }
};
```
-----
# 238. Product of Array Except Self

Medium

Given an integer array nums, return an array answer such that answer[i] is equal to the product of all the elements of nums except nums[i].

The product of any prefix or suffix of nums is guaranteed to fit in a 32-bit integer.

You must write an algorithm that runs in O(n) time and without using the division operation.

 

#### Example 1:

Input: nums = [1,2,3,4] <br/>
Output: [24,12,8,6] <br/>

#### Example 2:

Input: nums = [-1,1,0,-3,3] <br/>
Output: [0,0,9,0,0] <br/>
 

Constraints:

2 <= nums.length <= 105
-30 <= nums[i] <= 30
The input is generated such that answer[i] is guaranteed to fit in a 32-bit integer.


# Code
```cpp []
class Solution {
 public:
  vector<int> productExceptSelf(vector<int>& nums) {
    const int n = nums.size();
    vector<int> ans(n);        
    vector<int> prefix(n, 1);  
    vector<int> suffix(n, 1);  

    for(int i=1 ; i<n ; ++i){
        prefix[i] = prefix[i-1] * nums[i-1];
    }

    for(int i = n-2 ; i>=0 ; --i){
        suffix[i] = suffix[i+1] * nums[i+1];
    }

    for(int i=0 ; i<n ; ++i){
        ans[i] = prefix[i] * suffix[i];
    }


    return ans;
  }
};
```
----
# 53. Maximum Subarray

Medium

Given an integer array nums, find the subarray with the largest sum, and return its sum.

 

#### Example 1:

Input: nums = [-2,1,-3,4,-1,2,1,-5,4] <br/>
Output: 6 <br/>
Explanation: The subarray [4,-1,2,1] has the largest sum 6. <br/>

#### Example 2:

Input: nums = [1] <br/>
Output: 1 <br/>
Explanation: The subarray [1] has the largest sum 1. <br/>

#### Example 3:

Input: nums = [5,4,-1,7,8] <br/>
Output: 23 <br/>
Explanation: The subarray [5,4,-1,7,8] has the largest sum 23. <br/>
 

Constraints:

1 <= nums.length <= 105
-104 <= nums[i] <= 104

# Code
```cpp []
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int ans = INT_MIN;
        int sum = 0;

        for(int i=0 ; i<nums.size() ; ++i){
            
            sum+=nums[i];

            ans = max(sum,ans);

            if(sum<0){
                sum = 0;
            }
        }

        return ans;
    }
};
```
----
# 152. Maximum Product Subarray

Medium

Given an integer array nums, find a subarray that has the largest product, and return the product.

The test cases are generated so that the answer will fit in a 32-bit integer.

 

#### Example 1:

Input: nums = [2,3,-2,4] <br/>
Output: 6 <br/>
Explanation: [2,3] has the largest product 6. <br/>

#### Example 2:

Input: nums = [-2,0,-1] <br/>
Output: 0 <br/>
Explanation: The result cannot be 2, because [-2,-1] is not a subarray. <br/>
 

Constraints:

1 <= nums.length <= 2 * 104
-10 <= nums[i] <= 10
The product of any subarray of nums is guaranteed to fit in a 32-bit integer.

# Code
```cpp []
class Solution {
public:
    int maxProduct(vector<int>& nums) {
        int l = nums.size();

        int ans = INT_MIN;
        
        int pre = 1;
        int suf = 1;

        for(int i=0 ; i<l ; ++i){

            if(pre == 0) pre = 1;
            if(suf == 0 ) suf = 1;

            pre *= nums[i];
            suf *= nums[l-i-1];

            ans = max(ans,max(pre,suf));
        }
        

        return ans;
    }
};
```
---
# 153. Find Minimum in Rotated Sorted Array

Medium

Suppose an array of length n sorted in ascending order is rotated between 1 and n times. For example, the array nums = [0,1,2,4,5,6,7] might become:

[4,5,6,7,0,1,2] if it was rotated 4 times.
[0,1,2,4,5,6,7] if it was rotated 7 times.
Notice that rotating an array [a[0], a[1], a[2], ..., a[n-1]] 1 time results in the array [a[n-1], a[0], a[1], a[2], ..., a[n-2]].

Given the sorted rotated array nums of unique elements, return the minimum element of this array.

You must write an algorithm that runs in O(log n) time.

 
#### Example 1:

Input: nums = [3,4,5,1,2] <br/>
Output: 1 <br/>
Explanation: The original array was [1,2,3,4,5] rotated 3 times. <br/>

#### Example 2:

Input: nums = [4,5,6,7,0,1,2] <br/>
Output: 0 <br/>
Explanation: The original array was [0,1,2,4,5,6,7] and it was rotated 4 times. <br/>

#### Example 3:

Input: nums = [11,13,15,17] <br/>
Output: 11 <br/>
Explanation: The original array was [11,13,15,17] and it was rotated 4 times.  <br/>
 

Constraints:

n == nums.length
1 <= n <= 5000
-5000 <= nums[i] <= 5000
All the integers of nums are unique.
nums is sorted and rotated between 1 and n times.

# Code
```cpp []
class Solution {
public:
    int findMin(vector<int>& nums) {

        int ans = INT_MAX;

        int l = 0;
        int h = nums.size() - 1;

        while(l <= h){
            int m = (l + h )/2;

            if(nums[l] <= nums[m] ){
                ans = min(ans,nums[l]);
                l = m + 1;
            }
            else{
                ans = min(ans,nums[m]);
                h = m - 1;
            }
        }
      

        return ans;
    }
};
```
----
# 33. Search in Rotated Sorted Array

Medium

There is an integer array nums sorted in ascending order (with distinct values).

Prior to being passed to your function, nums is possibly rotated at an unknown pivot index k (1 <= k < nums.length) such that the resulting array is [nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]] (0-indexed). For example, [0,1,2,4,5,6,7] might be rotated at pivot index 3 and become [4,5,6,7,0,1,2].

Given the array nums after the possible rotation and an integer target, return the index of target if it is in nums, or -1 if it is not in nums.

You must write an algorithm with O(log n) runtime complexity.

 

#### Example 1:

Input: nums = [4,5,6,7,0,1,2], target = 0 <br/>
Output: 4 <br/>

#### Example 2:

Input: nums = [4,5,6,7,0,1,2], target = 3 <br/>
Output: -1 <br/>

#### Example 3:

Input: nums = [1], target = 0 <br/>
Output: -1 <br/>
 

Constraints:

1 <= nums.length <= 5000
-104 <= nums[i] <= 104
All values of nums are unique.
nums is an ascending array that is possibly rotated.
-104 <= target <= 104

# Code
```cpp []
class Solution {
public:
    int search(vector<int>& nums, int target) {

        int ans = -1;
        int n = nums.size();
        int l = 0 , h = n - 1;

        while(l <= h){
            int m = (l+h) / 2;

            if(nums[m] == target){
                ans = m;
                break;
            }

            if(nums[l] <= nums[m]){
                if(nums[l] <= target && target <= nums[m]){
                    h = m ;
                }
                else{
                    l = m + 1;
                }
            }
            else{
                if(nums[m] <= target && target <= nums[h]){
                    l = m;
                }else{
                    h = m - 1;
                }
            }
           
        }

        return ans;
    }
};
```
-----
# 15. 3Sum

Medium

Given an integer array nums, return all the triplets [nums[i], nums[j], nums[k]] such that i != j, i != k, and j != k, and nums[i] + nums[j] + nums[k] == 0.

Notice that the solution set must not contain duplicate triplets.

 

#### Example 1:

Input: nums = [-1,0,1,2,-1,-4] <br/>
Output: [[-1,-1,2],[-1,0,1]] <br/>
Explanation:  <br/>
nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0. <br/>
nums[1] + nums[2] + nums[4] = 0 + 1 + (-1) = 0. <br/>
nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0. <br/>
The distinct triplets are [-1,0,1] and [-1,-1,2]. <br/>
Notice that the order of the output and the order of the triplets does not matter.

#### Example 2:

Input: nums = [0,1,1] <br/>
Output: [] <br/>
Explanation: The only possible triplet does not sum up to 0. <br/>

#### Example 3:

Input: nums = [0,0,0] <br/>
Output: [[0,0,0]] <br/>
Explanation: The only possible triplet sums up to 0. <br/>
 

Constraints:

3 <= nums.length <= 3000
-105 <= nums[i] <= 105

# Code
```cpp []
    class Solution {
    public:
        vector<vector<int>> threeSum(vector<int>& nums) { 

            vector<vector<int>> ans;

            sort(nums.begin(),nums.end());

            int n = nums.size();

            for(int i = 0 ; i < n ; ++i){
                if(i>0 && nums[i] == nums[i-1]) continue;

                int j = i + 1;
                int k = n - 1;

                while( j < k){
                    int sum = nums[i] + nums[j] + nums[k];
                    if(sum < 0) j++;
                    else if(sum > 0) k--;
                    else{
                        vector<int> temp = {nums[i],nums[j],nums[k]};
                        ans.push_back(temp);
                        j++;
                        k--;
                        while( j<k && nums[j] == nums[j-1]) j++;
                        while( j<k && nums[k] == nums[k+1]) k--;
                    }
                }
            }
            
            return ans; 
        }
    };

```
----
# 11. Container With Most Water

Medium

You are given an integer array height of length n. There are n vertical lines drawn such that the two endpoints of the ith line are (i, 0) and (i, height[i]).

Find two lines that together with the x-axis form a container, such that the container contains the most water.

Return the maximum amount of water a container can store.

Notice that you may not slant the container.

 

#### Example 1:


Input: height = [1,8,6,2,5,4,8,3,7] <br/>
Output: 49 <br/>
Explanation: The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49. <br/>

#### Example 2:

Input: height = [1,1] <br/>
Output: 1 <br/>
 

Constraints:

n == height.length
2 <= n <= 105
0 <= height[i] <= 104

# Code
```cpp []
class Solution {
public:
    int maxArea(vector<int>& arr) {
        int ans = 0;
        int n = arr.size();
        int l = 0 , r = n - 1;

        while( l < r){
            int amt  = min(arr[l],arr[r]) * (r - l);
            ans = max(ans,amt);

            if(arr[l] < arr[r]){
                l++;
            }else{
                r--;
            }
        }

        return ans;
    }
};
```
----

# 3068. Find the Maximum Sum of Node Values

Hard

There exists an undirected tree with n nodes numbered 0 to n - 1. You are given a 0-indexed 2D integer array edges of length n - 1, where edges[i] = [ui, vi] indicates that there is an edge between nodes ui and vi in the tree. You are also given a positive integer k, and a 0-indexed array of non-negative integers nums of length n, where nums[i] represents the value of the node numbered i.

Alice wants the sum of values of tree nodes to be maximum, for which Alice can perform the following operation any number of times (including zero) on the tree:

Choose any edge [u, v] connecting the nodes u and v, and update their values as follows:
nums[u] = nums[u] XOR k
nums[v] = nums[v] XOR k
Return the maximum possible sum of the values Alice can achieve by performing the operation any number of times.

 

#### Example 1:


Input: nums = [1,2,1], k = 3, edges = [[0,1],[0,2]] <br/>
Output: 6 <br/>
Explanation: Alice can achieve the maximum sum of 6 using a single operation: <br/>
- Choose the edge [0,2]. nums[0] and nums[2] become: 1 XOR 3 = 2, and the array nums becomes: [1,2,1] -> [2,2,2]. <br/>
The total sum of values is 2 + 2 + 2 = 6. <br/>
It can be shown that 6 is the maximum achievable sum of values.

#### Example 2:


Input: nums = [2,3], k = 7, edges = [[0,1]] <br/>
Output: 9 <br/>
Explanation: Alice can achieve the maximum sum of 9 using a single operation: <br/>
- Choose the edge [0,1]. nums[0] becomes: 2 XOR 7 = 5 and nums[1] become: 3 XOR 7 = 4, and the array nums becomes: [2,3] -> [5,4]. <br/>
The total sum of values is 5 + 4 = 9. <br/>
It can be shown that 9 is the maximum achievable sum of values. <br/>

#### Example 3:


Input: nums = [7,7,7,7,7,7], k = 3, edges = [[0,1],[0,2],[0,3],[0,4],[0,5]] <br/>
Output: 42 <br/>
Explanation: The maximum achievable sum is 42 which can be achieved by Alice performing no operations. <br/>
 

Constraints:

2 <= n == nums.length <= 2 * 104
1 <= k <= 109
0 <= nums[i] <= 109
edges.length == n - 1
edges[i].length == 2
0 <= edges[i][0], edges[i][1] <= n - 1
The input is generated such that edges represent a valid tree.

# Code
```cpp []
class Solution {
 public:
  long long maximumValueSum(vector<int>& nums, int k,
                            vector<vector<int>>& edges) {
    long maxSum = 0;
    int changedCount = 0;
    int minChangeDiff = INT_MAX;

    for (const int num : nums) {
      maxSum += max(num, num ^ k);
      changedCount += ((num ^ k) > num) ? 1 : 0;
      minChangeDiff = min(minChangeDiff, abs(num - (num ^ k)));
    }

    if (changedCount % 2 == 0)
      return maxSum;
    return maxSum - minChangeDiff;
  }
};
```
-----
# 371. Sum of Two Integers [Link🚀](https://leetcode.com/problems/sum-of-two-integers/description/)
Medium

Given two integers a and b, return the sum of the two integers without using the operators + and -.

 

#### Example 1:

Input: a = 1, b = 2 <br/>
Output: 3 <br/>

#### Example 2:

Input: a = 2, b = 3 <br/>
Output: 5 <br/>
 

Constraints:

-1000 <= a, b <= 1000

# Code
```cpp []
class Solution {
 public:
  int getSum(unsigned a, unsigned b) {
    while (b != 0) {                 
      const unsigned carry = a & b;  
      a ^= b;  
      b = carry << 1;
    }
    return a;
  }
};
```
----

# 191. Number of 1 Bits [Link🚀](https://leetcode.com/problems/number-of-1-bits/description/)
Easy

Given a positive integer n, write a function that returns the number of set bits in its binary representation (also known as the Hamming weight).

 

Example 1:

Input: n = 11

Output: 3

Explanation:

The input binary string 1011 has a total of three set bits.

Example 2:

Input: n = 128

Output: 1

Explanation:

The input binary string 10000000 has a total of one set bit.

Example 3:

Input: n = 2147483645

Output: 30

Explanation:

The input binary string 1111111111111111111111111111101 has a total of thirty set bits.

 

Constraints:

1 <= n <= 231 - 1

# Code
```cpp []
class Solution {
public:
    int hammingWeight(int n) {
        int ans = 0;

        while(n){
            n &= (n-1);
            ans++;
        }

        return ans;
    }
};
```
----
# 338. Counting Bits [Link🚀](https://leetcode.com/problems/counting-bits/description/)
Easy

Given an integer n, return an array ans of length n + 1 such that for each i (0 <= i <= n), ans[i] is the number of 1's in the binary representation of i.

 

Example 1:

Input: n = 2
Output: [0,1,1]
Explanation:
0 --> 0
1 --> 1
2 --> 10
Example 2:

Input: n = 5
Output: [0,1,1,2,1,2]
Explanation:
0 --> 0
1 --> 1
2 --> 10
3 --> 11
4 --> 100
5 --> 101
 

Constraints:

0 <= n <= 105


# Code
```cpp []
class Solution {
 public:
  vector<int> countBits(int n) {

    vector<int> ans(n+1,0);

    for(int i = 1 ; i<=n ; ++i){
        ans[i] = ans[i/2] + ( i & 1);
    }

    return ans;
  }
};
```
----
