# leetcode march-2025

----

# 1749. Maximum Absolute Sum of Any Subarray
Solved
Medium

You are given an integer array nums. The absolute sum of a subarray [numsl, numsl+1, ..., numsr-1, numsr] is abs(numsl + numsl+1 + ... + numsr-1 + numsr).

Return the maximum absolute sum of any (possibly empty) subarray of nums.

Note that abs(x) is defined as follows:

If x is a negative integer, then abs(x) = -x.
If x is a non-negative integer, then abs(x) = x.
 

#### Example 1:

Input: nums = [1,-3,2,3,-4] <br/>
Output: 5 <br/>
Explanation: The subarray [2,3] has absolute sum = abs(2+3) = abs(5) = 5. <br/>

#### Example 2:

Input: nums = [2,-5,1,-4,3,-2] <br/>
Output: 8 <br/>
Explanation: The subarray [-5,1,-4] has absolute sum = abs(-5+1-4) = abs(-8) = 8.
 

Constraints:

1 <= nums.length <= 105
-104 <= nums[i] <= 104

# Code
```java []
class Solution {
  public int maxAbsoluteSum(int[] nums) {
    int ans = Integer.MIN_VALUE;
    int maxSum = 0;
    int minSum = 0;

    for (final int num : nums) {
      maxSum = Math.max(num, maxSum + num);
      minSum = Math.min(num, minSum + num);
      ans = Math.max(ans, Math.max(maxSum, -minSum));
    }

    return ans;
  }
}
```
---
# 873. Length of Longest Fibonacci Subsequence
Solved
Medium

A sequence x1, x2, ..., xn is Fibonacci-like if:

n >= 3
xi + xi+1 == xi+2 for all i + 2 <= n
Given a strictly increasing array arr of positive integers forming a sequence, return the length of the longest Fibonacci-like subsequence of arr. If one does not exist, return 0.

A subsequence is derived from another sequence arr by deleting any number of elements (including none) from arr, without changing the order of the remaining elements. For example, [3, 5, 8] is a subsequence of [3, 4, 5, 6, 7, 8].

 

#### Example 1:

Input: arr = [1,2,3,4,5,6,7,8] <br/>
Output: 5 <br/>
Explanation: The longest subsequence that is fibonacci-like: [1,2,3,5,8]. <br/>

#### Example 2:

Input: arr = [1,3,7,11,12,14,18] <br/>
Output: 3 <br/>
Explanation: The longest subsequence that is fibonacci-like: [1,11,12], [3,11,14] or [7,11,18]. <br/>
 

Constraints:

3 <= arr.length <= 1000
1 <= arr[i] < arr[i + 1] <= 109

# Code
```java []
class Solution {
  public int lenLongestFibSubseq(int[] arr) {
    final int n = arr.length;
    int ans = 0;
    int[][] dp = new int[n][n];
    Arrays.stream(dp).forEach(A -> Arrays.fill(A, 2));
    Map<Integer, Integer> numToIndex = new HashMap<>();

    for (int i = 0; i < n; ++i)
      numToIndex.put(arr[i], i);

    for (int j = 0; j < n; ++j)
      for (int k = j + 1; k < n; ++k) {
        final int ai = arr[k] - arr[j];
        if (ai < arr[j] && numToIndex.containsKey(ai)) {
          final int i = numToIndex.get(ai);
          dp[j][k] = dp[i][j] + 1;
          ans = Math.max(ans, dp[j][k]);
        }
      }

    return ans;
  }
}
```
---
# 2570. Merge Two 2D Arrays by Summing Values
Solved
Easy

You are given two 2D integer arrays nums1 and nums2.

nums1[i] = [idi, vali] indicate that the number with the id idi has a value equal to vali.
nums2[i] = [idi, vali] indicate that the number with the id idi has a value equal to vali.
Each array contains unique ids and is sorted in ascending order by id.

Merge the two arrays into one array that is sorted in ascending order by id, respecting the following conditions:

Only ids that appear in at least one of the two arrays should be included in the resulting array.
Each id should be included only once and its value should be the sum of the values of this id in the two arrays. If the id does not exist in one of the two arrays, then assume its value in that array to be 0.
Return the resulting array. The returned array must be sorted in ascending order by id.

 

#### Example 1:

Input: nums1 = [[1,2],[2,3],[4,5]], nums2 = [[1,4],[3,2],[4,1]] <br/>
Output: [[1,6],[2,3],[3,2],[4,6]] <br/>
Explanation: The resulting array contains the following: <br/>
- id = 1, the value of this id is 2 + 4 = 6. <br/>
- id = 2, the value of this id is 3. <br/>
- id = 3, the value of this id is 2. <br/>
- id = 4, the value of this id is 5 + 1 = 6. <br/>

#### Example 2:

Input: nums1 = [[2,4],[3,6],[5,5]], nums2 = [[1,3],[4,3]] <br/>
Output: [[1,3],[2,4],[3,6],[4,3],[5,5]] <br/>
Explanation: There are no common ids, so we just include each id with its value in the resulting list. <br/>
 

##### Constraints:

1 <= nums1.length, nums2.length <= 200
nums1[i].length == nums2[j].length == 2
1 <= idi, vali <= 1000
Both arrays contain unique ids.
Both arrays are in strictly ascending order by id.

# Code
```java []
class Solution {
  public int[][] mergeArrays(int[][] nums1, int[][] nums2) {
    final int kMax = 1000;
    List<int[]> ans = new ArrayList<>();
    int[] count = new int[kMax + 1];

    addCount(nums1, count);
    addCount(nums2, count);

    for (int i = 1; i <= kMax; ++i)
      if (count[i] > 0)
        ans.add(new int[] {i, count[i]});

    return ans.stream().toArray(int[][] ::new);
  }

  private void addCount(int[][] nums, int[] count) {
    for (int[] idAndVal : nums) {
      final int id = idAndVal[0];
      final int val = idAndVal[1];
      count[id] += val;
    }
  }
}
```
---
# 2965. Find Missing and Repeated Values
Solved
Easy

You are given a 0-indexed 2D integer matrix grid of size n * n with values in the range [1, n2]. Each integer appears exactly once except a which appears twice and b which is missing. The task is to find the repeating and missing numbers a and b.

Return a 0-indexed integer array ans of size 2 where ans[0] equals to a and ans[1] equals to b.

 

#### Example 1:

Input: grid = [[1,3],[2,2]] <br/>
Output: [2,4] <br/>
Explanation: Number 2 is repeated and number 4 is missing so the answer is [2,4]. <br/>

#### Example 2:

Input: grid = [[9,1,7],[8,9,2],[3,4,6]] <br/>
Output: [9,5] <br/>
Explanation: Number 9 is repeated and number 5 is missing so the answer is [9,5].
 

Constraints:

2 <= n == grid.length == grid[i].length <= 50
1 <= grid[i][j] <= n * n
For all x that 1 <= x <= n * n there is exactly one x that is not equal to any of the grid members.
For all x that 1 <= x <= n * n there is exactly one x that is equal to exactly two of the grid members.
For all x that 1 <= x <= n * n except two of them there is exatly one pair of i, j that 0 <= i, j <= n - 1 and grid[i][j] == x.

# Code
```java []
class Solution {
  public int[] findMissingAndRepeatedValues(int[][] grid) {
    final int n = grid.length;
    final int nSquared = n * n;
    int[] count = new int[nSquared + 1];

    for (int[] row : grid)
      for (final int num : row)
        ++count[num];

    int repeated = -1;
    int missing = -1;

    for (int i = 1; i <= nSquared; ++i) {
      if (count[i] == 2)
        repeated = i;
      if (count[i] == 0)
        missing = i;
    }

    return new int[] {repeated, missing};
  }
}
```
----
