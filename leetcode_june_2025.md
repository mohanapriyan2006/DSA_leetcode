

# Quick Sort -> [link](https://www.geeksforgeeks.org/problems/quick-sort/1) (GFG)

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

# Largest Element in Array -> [Link](https://www.geeksforgeeks.org/problems/largest-element-in-array4009/1) (GFG)

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
# 1752. Check if Array Is Sorted and Rotated -> [LINK](https://leetcode.com/problems/check-if-array-is-sorted-and-rotated/description)

Easy

Given an array nums, return true if the array was originally sorted in non-decreasing order, then rotated some number of positions (including zero). Otherwise, return false.

There may be duplicates in the original array.

Note: An array A rotated by x positions results in an array B of the same length such that B[i] == A[(i+x) % A.length] for every valid index i.
 

Example 1:

Input: nums = [3,4,5,1,2]
Output: true
Explanation: [1,2,3,4,5] is the original sorted array.
You can rotate the array by x = 3 positions to begin on the element of value 3: [3,4,5,1,2].
Example 2:

Input: nums = [2,1,3,4]
Output: false
Explanation: There is no sorted array once rotated that can make nums.
Example 3:

Input: nums = [1,2,3]
Output: true
Explanation: [1,2,3] is the original sorted array.
You can rotate the array by x = 0 positions (i.e. no rotation) to make nums. 

Constraints:

1 <= nums.length <= 100
1 <= nums[i] <= 100

# Code
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
-----


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
# 189. Rotate Array -> [LINK](https://leetcode.com/problems/rotate-array/description/)

Medium

Given an integer array nums, rotate the array to the right by k steps, where k is non-negative.

 

Example 1:

Input: nums = [1,2,3,4,5,6,7], k = 3
Output: [5,6,7,1,2,3,4]

Explanation:
rotate 1 steps to the right: [7,1,2,3,4,5,6]
rotate 2 steps to the right: [6,7,1,2,3,4,5]
rotate 3 steps to the right: [5,6,7,1,2,3,4]

Example 2:

Input: nums = [-1,-100,3,99], k = 2
Output: [3,99,-1,-100]

Explanation: 
rotate 1 steps to the right: [99,-1,-100,3]
rotate 2 steps to the right: [3,99,-1,-100]
 

Constraints:

1 <= nums.length <= 105
-231 <= nums[i] <= 231 - 1
0 <= k <= 105
 

Follow up:

Try to come up with as many solutions as you can. There are at least three different ways to solve this problem.
Could you do it in-place with O(1) extra space?

# Code
```cpp []
class Solution {
 public:
  void rotate(vector<int>& arr, int k) {
    int n = arr.size();
    k %= n;
    reverse(arr,0,n-1);
    reverse(arr,0,k-1);
    reverse(arr,k,n-1);
  }

  private:
  void  reverse(vector<int>& nums,int l,int h){
    while(l<h) swap(nums[l++],nums[h--]);
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
