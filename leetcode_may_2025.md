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
