
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

# 3443. Maximum Manhattan Distance After K Changes -> [LeetCode](https://leetcode.com/problems/maximum-manhattan-distance-after-k-changes/description/)

Medium

You are given a string s consisting of the characters 'N', 'S', 'E', and 'W', where s[i] indicates movements in an infinite grid:

'N' : Move north by 1 unit.
'S' : Move south by 1 unit.
'E' : Move east by 1 unit.
'W' : Move west by 1 unit.
Initially, you are at the origin (0, 0). You can change at most k characters to any of the four directions.

Find the maximum Manhattan distance from the origin that can be achieved at any time while performing the movements in order.

The Manhattan Distance between two cells (xi, yi) and (xj, yj) is |xi - xj| + |yi - yj|.
 

Example 1:

Input: s = "NWSE", k = 1

Output: 3

Explanation:

Change s[2] from 'S' to 'N'. The string s becomes "NWNE".

Movement	Position (x, y)	Manhattan Distance	Maximum
s[0] == 'N'	(0, 1)	0 + 1 = 1	1
s[1] == 'W'	(-1, 1)	1 + 1 = 2	2
s[2] == 'N'	(-1, 2)	1 + 2 = 3	3
s[3] == 'E'	(0, 2)	0 + 2 = 2	3
The maximum Manhattan distance from the origin that can be achieved is 3. Hence, 3 is the output.

Example 2:

Input: s = "NSWWEW", k = 3

Output: 6

Explanation:

Change s[1] from 'S' to 'N', and s[4] from 'E' to 'W'. The string s becomes "NNWWWW".

The maximum Manhattan distance from the origin that can be achieved is 6. Hence, 6 is the output.

 

Constraints:

1 <= s.length <= 105
0 <= k <= s.length
s consists of only 'N', 'S', 'E', and 'W'.

# Code
```cpp []
class Solution {
 public:
  int maxDistance(string s, int k) {
    return max({flip(s, k, "NE"), flip(s, k, "NW"),  //
                flip(s, k, "SE"), flip(s, k, "SW")});
  }

 private:
  int flip(const string& s, int k, const string& direction) {
    int res = 0;
    int pos = 0;
    int opposite = 0;

    for (const char c : s) {
      if (direction.find(c) != string::npos) {
        ++pos;
      } else {
        --pos;
        ++opposite;
      }
      res = max(res, pos + 2 * min(k, opposite));
    }

    return res;
  }
};
```
-----

# 3085. Minimum Deletions to Make String K-Special -> [LeetCode](https://leetcode.com/problems/minimum-deletions-to-make-string-k-special/description/)

Medium

You are given a string word and an integer k.

We consider word to be k-special if |freq(word[i]) - freq(word[j])| <= k for all indices i and j in the string.

Here, freq(x) denotes the frequency of the character x in word, and |y| denotes the absolute value of y.

Return the minimum number of characters you need to delete to make word k-special.

 

Example 1:

Input: word = "aabcaba", k = 0

Output: 3

Explanation: We can make word 0-special by deleting 2 occurrences of "a" and 1 occurrence of "c". Therefore, word becomes equal to "baba" where freq('a') == freq('b') == 2.

Example 2:

Input: word = "dabdcbdcdcd", k = 2

Output: 2

Explanation: We can make word 2-special by deleting 1 occurrence of "a" and 1 occurrence of "d". Therefore, word becomes equal to "bdcbdcdcd" where freq('b') == 2, freq('c') == 3, and freq('d') == 4.

Example 3:

Input: word = "aaabaaa", k = 2

Output: 1

Explanation: We can make word 2-special by deleting 1 occurrence of "b". Therefore, word becomes equal to "aaaaaa" where each letter's frequency is now uniformly 6.

 

Constraints:

1 <= word.length <= 105
0 <= k <= 105
word consists only of lowercase English letters.

# Code
```cpp []
class Solution {
 public:
  int minimumDeletions(string word, int k) {
    int ans = INT_MAX;
    vector<int> count(26);

    for (const char c : word)
      ++count[c - 'a'];

    for (const int minFreq : count) {
      int deletions = 0;
      for (const int freq : count)
        if (freq < minFreq)  // Delete all the letters with smaller frequency.
          deletions += freq;
        else  // Delete letters with exceeding frequency.
          deletions += max(0, freq - (minFreq + k));
      ans = min(ans, deletions);
    }

    return ans;
  }
};
```
----

# 219. Contains Duplicate II -> [LeetCode](https://leetcode.com/problems/contains-duplicate-ii/description/)

Easy

Given an integer array nums and an integer k, return true if there are two distinct indices i and j in the array such that nums[i] == nums[j] and abs(i - j) <= k.

 

Example 1:

Input: nums = [1,2,3,1], k = 3
Output: true
Example 2:

Input: nums = [1,0,1,1], k = 1
Output: true
Example 3:

Input: nums = [1,2,3,1,2,3], k = 2
Output: false
 

Constraints:

1 <= nums.length <= 105
-109 <= nums[i] <= 109
0 <= k <= 105

# Code
```cpp []
class Solution {
 public:
  bool containsNearbyDuplicate(vector<int>& nums, int k) {
    unordered_set<int> seen;

    for (int i = 0; i < nums.size(); ++i) {
      if (!seen.insert(nums[i]).second)
        return true;
      if (i >= k)
        seen.erase(nums[i - k]);
    }

    return false;
  }
};
```
-----


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

# 2138. Divide a String Into Groups of Size k -> [LeetCode](https://leetcode.com/problems/divide-a-string-into-groups-of-size-k/description/)

Easy

A string s can be partitioned into groups of size k using the following procedure:

The first group consists of the first k characters of the string, the second group consists of the next k characters of the string, and so on. Each element can be a part of exactly one group.
For the last group, if the string does not have k characters remaining, a character fill is used to complete the group.
Note that the partition is done so that after removing the fill character from the last group (if it exists) and concatenating all the groups in order, the resultant string should be s.

Given the string s, the size of each group k and the character fill, return a string array denoting the composition of every group s has been divided into, using the above procedure.

 

Example 1:

Input: s = "abcdefghi", k = 3, fill = "x"
Output: ["abc","def","ghi"]
Explanation:
The first 3 characters "abc" form the first group.
The next 3 characters "def" form the second group.
The last 3 characters "ghi" form the third group.
Since all groups can be completely filled by characters from the string, we do not need to use fill.
Thus, the groups formed are "abc", "def", and "ghi".
Example 2:

Input: s = "abcdefghij", k = 3, fill = "x"
Output: ["abc","def","ghi","jxx"]
Explanation:
Similar to the previous example, we are forming the first three groups "abc", "def", and "ghi".
For the last group, we can only use the character 'j' from the string. To complete this group, we add 'x' twice.
Thus, the 4 groups formed are "abc", "def", "ghi", and "jxx".
 

Constraints:

1 <= s.length <= 100
s consists of lowercase English letters only.
1 <= k <= 100
fill is a lowercase English letter.



# Code
```cpp []
class Solution {
 public:
  vector<string> divideString(string s, int k, char fill) {

    vector<string> ans;

    for (int i = 0; i < s.length(); i += k)
      ans.push_back(i + k > s.length()
                        ? s.substr(i) + string(i + k - s.length(), fill)
                        : s.substr(i, k));

    return ans;
    
  }
};
```
------

