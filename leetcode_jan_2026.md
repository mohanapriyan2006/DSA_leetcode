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


# [1975. Maximum Matrix Sum](https://leetcode.com/problems/maximum-matrix-sum/)

Medium
 
You are given an n x n integer matrix. You can do the following operation any number of times:

Choose any two adjacent elements of matrix and multiply each of them by -1.
Two elements are considered adjacent if and only if they share a border.

Your goal is to maximize the summation of the matrix's elements. Return the maximum sum of the matrix's elements using the operation mentioned above.

 

Example 1:

![img](https://assets.leetcode.com/uploads/2021/07/16/pc79-q2ex1.png)

Input: matrix = [[1,-1],[-1,1]]

Output: 4

Explanation: We can follow the following steps to reach sum equals 4:
- Multiply the 2 elements in the first row by -1.
- Multiply the 2 elements in the first column by -1.



Example 2:

![img](https://assets.leetcode.com/uploads/2021/07/16/pc79-q2ex2.png)

Input: matrix = [[1,2,3],[-1,-2,-3],[1,2,3]]

Output: 16

Explanation: We can follow the following step to reach sum equals 16:

- Multiply the 2 last elements in the second row by -1.
 

Constraints:

n == matrix.length == matrix[i].length
2 <= n <= 250
-105 <= matrix[i][j] <= 105


# Code
```cpp []
class Solution {
public:
    long long maxMatrixSum(vector<vector<int>>& matrix) {
        int minValue = INT_MAX;
        long long sum = 0;
        int negCount = 0;

        for (int i = 0; i < matrix.size(); i++) {
            for (int j = 0; j < matrix[0].size(); j++) {
                if (matrix[i][j] < 0)
                    negCount++;
                int absValue = abs(matrix[i][j]);
                minValue = min(minValue, absValue);
                sum += absValue;
            }
        }

        if (negCount % 2 == 0)
            return sum;
        return sum - 2 * minValue;
    }
};
```

------------------------------------------------------------------------------------------------------------------------


# [1161. Maximum Level Sum of a Binary Tree](https://leetcode.com/problems/maximum-level-sum-of-a-binary-tree)

Medium

Given the root of a binary tree, the level of its root is 1, the level of its children is 2, and so on.

Return the smallest level x such that the sum of all the values of nodes at level x is maximal.

 

Example 1:

![img](https://assets.leetcode.com/uploads/2019/05/03/capture.JPG)

Input: root = [1,7,0,7,-8,null,null]

Output: 2

Explanation: 

Level 1 sum = 1.
Level 2 sum = 7 + 0 = 7.
Level 3 sum = 7 + -8 = -1.
So we return the level with the maximum sum which is level 2.
\


Example 2:

Input: root = [989,null,10250,98693,-89388,null,null,null,-32127]

Output: 2
 

Constraints:

The number of nodes in the tree is in the range [1, 104].
-105 <= Node.val <= 105



# Code
```cpp []
class Solution {
public:
    int maxLevelSum(TreeNode* root) {
        if (root == nullptr) {
            return 0;
        }

        std::queue<TreeNode*> queue;
        queue.push(root);
        int maxLevel = 1;
        int maxSum = INT_MIN;
        int level = 1;

        while (!queue.empty()) {
            int levelSum = 0;
            int levelSize = queue.size();

            for (int i = 0; i < levelSize; i++) {
                TreeNode* node = queue.front();
                queue.pop();
                levelSum += node->val;

                if (node->left != nullptr) {
                    queue.push(node->left);
                }
                if (node->right != nullptr) {
                    queue.push(node->right);
                }
            }

            if (levelSum > maxSum) {
                maxSum = levelSum;
                maxLevel = level;
            }

            level++;
        }

        return maxLevel;
    }
};
```

--------------------------------------------------------------------------------------------------------------------------------------


# [1458. Max Dot Product of Two Subsequences](https://leetcode.com/problems/max-dot-product-of-two-subsequences)

Hard
 
Given two arrays nums1 and nums2.

Return the maximum dot product between non-empty subsequences of nums1 and nums2 with the same length.

A subsequence of a array is a new array which is formed from the original array by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. (ie, [2,3,5] is a subsequence of [1,2,3,4,5] while [1,5,3] is not).

 

Example 1:

Input: nums1 = [2,1,-2,5], nums2 = [3,0,-6]

Output: 18

Explanation: Take subsequence [2,-2] from nums1 and subsequence [3,-6] from nums2.
Their dot product is (2*3 + (-2)*(-6)) = 18.



Example 2:

Input: nums1 = [3,-2], nums2 = [2,-6,7]

Output: 21

Explanation: Take subsequence [3] from nums1 and subsequence [7] from nums2.
Their dot product is (3*7) = 21.


Example 3:

Input: nums1 = [-1,-1], nums2 = [1,1]

Output: -1

Explanation: Take subsequence [-1] from nums1 and subsequence [1] from nums2.
Their dot product is -1.
 

Constraints:

1 <= nums1.length, nums2.length <= 500
-1000 <= nums1[i], nums2[i] <= 1000



# Code
```cpp []
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    vector<int> nums1, nums2;
    vector<vector<int>> memo;
    int n, m;
    const int NEG_INF = -1e9;

    int dp(int i, int j) {
        if (i == n || j == m)
            return NEG_INF;

        if (memo[i][j] != INT_MIN)
            return memo[i][j];

        int take = nums1[i] * nums2[j];

        int res = max({
            take + dp(i + 1, j + 1),
            take,                   
            dp(i + 1, j),         
            dp(i, j + 1) 
        });

        return memo[i][j] = res;
    }

    int maxDotProduct(vector<int>& a, vector<int>& b) {
        nums1 = a;
        nums2 = b;
        n = nums1.size();
        m = nums2.size();

        memo.assign(n, vector<int>(m, INT_MIN));
        return dp(0, 0);
    }
};
```



--------------------------------------------------------------------------------------------------------------------------



# [865. Smallest Subtree with all the Deepest Nodes](https://leetcode.com/problems/smallest-subtree-with-all-the-deepest-nodes)

Medium

Given the root of a binary tree, the depth of each node is the shortest distance to the root.

Return the smallest subtree such that it contains all the deepest nodes in the original tree.

A node is called the deepest if it has the largest depth possible among any node in the entire tree.

The subtree of a node is a tree consisting of that node, plus the set of all descendants of that node.

 

Example 1:

![img](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/01/sketch1.png)

Input: root = [3,5,1,6,2,0,8,null,null,7,4]

Output: [2,7,4]

Explanation: We return the node with value 2, colored in yellow in the diagram.
The nodes coloured in blue are the deepest nodes of the tree.
Notice that nodes 5, 3 and 2 contain the deepest nodes in the tree but node 2 is the smallest subtree among them, so we return it.



Example 2:

Input: root = [1]

Output: [1]

Explanation: The root is the deepest node in the tree.



Example 3:

Input: root = [0,1,3,null,2]

Output: [2]

Explanation: The deepest node in the tree is 2, the valid subtrees are the subtrees of nodes 2, 1 and 0 but the subtree of node 2 is the smallest.
 

Constraints:

The number of nodes in the tree will be in the range [1, 500].
0 <= Node.val <= 500
The values of the nodes in the tree are unique.



# Code
```cpp []
class Solution {
public:
    TreeNode* subtreeWithAllDeepest(TreeNode* root) {
        if (!root) return nullptr;

        unordered_map<TreeNode*, TreeNode*> parent;
        queue<TreeNode*> q;
        q.push(root);
        parent[root] = nullptr;

        vector<TreeNode*> lastLevel;

        while (!q.empty()) {
            int size = q.size();
            lastLevel.clear();

            for (int i = 0; i < size; i++) {
                TreeNode* node = q.front();
                q.pop();
                lastLevel.push_back(node);

                if (node->left) {
                    parent[node->left] = node;
                    q.push(node->left);
                }
                if (node->right) {
                    parent[node->right] = node;
                    q.push(node->right);
                }
            }
        }

        unordered_set<TreeNode*> deepest(lastLevel.begin(), lastLevel.end());

        while (deepest.size() > 1) {
            unordered_set<TreeNode*> next;
            for (auto node : deepest) {
                next.insert(parent[node]);
            }
            deepest = next;
        }

        return *deepest.begin();
    }
};
```


----------------------------------------------------------------------------------------------------------------------------


# [712. Minimum ASCII Delete Sum for Two Strings](https://leetcode.com/problems/minimum-ascii-delete-sum-for-two-strings)

Medium
 
Given two strings s1 and s2, return the lowest ASCII sum of deleted characters to make two strings equal.

 

Example 1:

Input: s1 = "sea", s2 = "eat"

Output: 231

Explanation: Deleting "s" from "sea" adds the ASCII value of "s" (115) to the sum.
Deleting "t" from "eat" adds 116 to the sum.
At the end, both strings are equal, and 115 + 116 = 231 is the minimum sum possible to achieve this.




Example 2:

Input: s1 = "delete", s2 = "leet"

Output: 403

Explanation: Deleting "dee" from "delete" to turn the string into "let",
adds 100[d] + 101[e] + 101[e] to the sum.
Deleting "e" from "leet" adds 101[e] to the sum.
At the end, both strings are equal to "let", and the answer is 100+101+101+101 = 403.
If instead we turned both strings into "lee" or "eet", we would get answers of 433 or 417, which are higher.
 

Constraints:

1 <= s1.length, s2.length <= 1000
s1 and s2 consist of lowercase English letters.


# Code
```cpp []
class Solution {
public:
    int minimumDeleteSum(string s1, string s2) {
        int m = s1.length();
        int n = s2.length();
        vector<int> dp(n + 1, 0);

        for (int j = 1; j <= n; j++) {
            dp[j] = dp[j - 1] + s2[j - 1];
        }

        for (int i = 1; i <= m; i++) {
            int prev = dp[0];
            dp[0] += s1[i - 1];

            for (int j = 1; j <= n; j++) {
                int temp = dp[j];

                if (s1[i - 1] == s2[j - 1]) {
                    dp[j] = prev;
                } else {
                    dp[j] = min(dp[j] + s1[i - 1], dp[j - 1] + s2[j - 1]);
                }

                prev = temp;
            }
        }

        return dp[n];        
    }
};
```


----------------------------------------------------------------------------------------------------------------------------


 # [85. Maximal Rectangle](https://leetcode.com/problems/maximal-rectangle/)
 
Hard
 
Given a rows x cols binary matrix filled with 0's and 1's, find the largest rectangle containing only 1's and return its area.

 

Example 1:

![img](https://leetcode.com/problems/maximal-rectangle/)

Input: matrix = [["1","0","1","0","0"],["1","0","1","1","1"],["1","1","1","1","1"],["1","0","0","1","0"]]

Output: 6

Explanation: The maximal rectangle is shown in the above picture.



Example 2:

Input: matrix = [["0"]]

Output: 0



Example 3:

Input: matrix = [["1"]]

Output: 1
 

Constraints:

rows == matrix.length
cols == matrix[i].length
1 <= rows, cols <= 200
matrix[i][j] is '0' or '1'.



# Code
```cpp []
class Solution {
public:
    int maximalRectangle(vector<vector<char>>& matrix) {
        if (matrix.empty() || matrix[0].empty())
            return 0;
        
        int rows = matrix.size();
        int cols = matrix[0].size();
        vector<int> heights(cols + 1, 0); 
        int maxArea = 0;
        
        for (const auto& row : matrix) {
            for (int i = 0; i < cols; i++) {
                heights[i] = (row[i] == '1') ? heights[i] + 1 : 0;
            }
            
            int n = heights.size(); 
            
            for (int i = 0; i < n; i++) {
                for (int j = i, minHeight = INT_MAX; j < n; j++) {
                    minHeight = min(minHeight, heights[j]);
                    int area = minHeight * (j - i + 1);
                    maxArea = max(maxArea, area);
                }
            }
        }
        
        return maxArea;
    }
};
```

-------------------------------------------------------------------------------------------------------------------------


# [1266. Minimum Time Visiting All Points](https://leetcode.com/problems/minimum-time-visiting-all-points)

Easy
 
On a 2D plane, there are n points with integer coordinates points[i] = [xi, yi]. Return the minimum time in seconds to visit all the points in the order given by points.

You can move according to these rules:

In 1 second, you can either:
move vertically by one unit,
move horizontally by one unit, or
move diagonally sqrt(2) units (in other words, move one unit vertically then one unit horizontally in 1 second).
You have to visit the points in the same order as they appear in the array.
You are allowed to pass through points that appear later in the order, but these do not count as visits.
 

Example 1:


Input: points = [[1,1],[3,4],[-1,0]]

Output: 7

![img](https://assets.leetcode.com/uploads/2019/11/14/1626_example_1.PNG)

Explanation: One optimal path is [1,1] -> [2,2] -> [3,3] -> [3,4] -> [2,3] -> [1,2] -> [0,1] -> [-1,0]   
Time from [1,1] to [3,4] = 3 seconds 
Time from [3,4] to [-1,0] = 4 seconds
Total time = 7 seconds



Example 2:

Input: points = [[3,2],[-2,2]]

Output: 5
 

Constraints:

points.length == n
1 <= n <= 100
points[i].length == 2
-1000 <= points[i][0], points[i][1] <= 1000



# Code
```cpp []
class Solution {
public:
    int minTimeToVisitAllPoints(vector<vector<int>>& points) {
        int res = 0;

        for (int i = 1; i < points.size(); i++) {
            res += max(
                abs(points[i][0] - points[i - 1][0]),
                abs(points[i][1] - points[i - 1][1])
            );
        }

        return res;        
    }
};
```

--------------------------------------------------------------------------------------------------------------------------


# [3453. Separate Squares I](https://leetcode.com/problems/separate-squares-i/)

Medium
 
You are given a 2D integer array squares. Each squares[i] = [xi, yi, li] represents the coordinates of the bottom-left point and the side length of a square parallel to the x-axis.

Find the minimum y-coordinate value of a horizontal line such that the total area of the squares above the line equals the total area of the squares below the line.

Answers within 10-5 of the actual answer will be accepted.

Note: Squares may overlap. Overlapping areas should be counted multiple times.

 

Example 1:

Input: squares = [[0,0,1],[2,2,1]]

Output: 1.00000

Explanation:

![img](https://assets.leetcode.com/uploads/2025/01/06/4062example1drawio.png)

Any horizontal line between y = 1 and y = 2 will have 1 square unit above it and 1 square unit below it. The lowest option is 1.



Example 2:

Input: squares = [[0,0,2],[1,1,1]]

Output: 1.16667

Explanation:

![img](https://assets.leetcode.com/uploads/2025/01/15/4062example2drawio.png)

The areas are:

Below the line: 7/6 * 2 (Red) + 1/6 (Blue) = 15/6 = 2.5.
Above the line: 5/6 * 2 (Red) + 5/6 (Blue) = 15/6 = 2.5.
Since the areas above and below the line are equal, the output is 7/6 = 1.16667.

 

Constraints:

1 <= squares.length <= 5 * 104
squares[i] = [xi, yi, li]
squares[i].length == 3
0 <= xi, yi <= 109
1 <= li <= 109
The total area of all the squares will not exceed 1012.



# Code
```cpp []
class Solution {
public:
    double helper(double line, vector<vector<int>>& squares){
        double aAbove = 0, aBelow = 0;
        int n = squares.size();
        for(int i = 0; i < n; i++){
            int x = squares[i][0], y = squares[i][1];
            int l = squares[i][2];
            double total = (double) l * l;
            
            if(line <= y){
                aAbove += total;
            } 
            else if(line >= y + l){
                aBelow += total;
            } 
            else{
                double aboveHeight = (y + l) - line;
                double belowHeight = line - y;
                aAbove += l * aboveHeight;
                aBelow += l * belowHeight;
            }
        }
        return aAbove - aBelow;
    }

    double separateSquares(vector<vector<int>>& squares) {
        double lo = 0, hi = 2*1e9;
        
        for(int i = 0; i < 60; i++){
            double mid = (lo + hi) / 2.0;
            double diff = helper(mid, squares);

            if(diff > 0) lo = mid;
            else hi = mid;
        }

        return hi;
    }
};
```

-------------------------------------------------------------------------------------------------------------------------

# 3454. Separate Squares II

Hard
 
You are given a 2D integer array squares. Each squares[i] = [xi, yi, li] represents the coordinates of the bottom-left point and the side length of a square parallel to the x-axis.

Find the minimum y-coordinate value of a horizontal line such that the total area covered by squares above the line equals the total area covered by squares below the line.

Answers within 10-5 of the actual answer will be accepted.

Note: Squares may overlap. Overlapping areas should be counted only once in this version.

 

Example 1:

Input: squares = [[0,0,1],[2,2,1]]

Output: 1.00000

Explanation:



Any horizontal line between y = 1 and y = 2 results in an equal split, with 1 square unit above and 1 square unit below. The minimum y-value is 1.




Example 2:

Input: squares = [[0,0,2],[1,1,1]]

Output: 1.00000

Explanation:



Since the blue square overlaps with the red square, it will not be counted again. Thus, the line y = 1 splits the squares into two equal parts.

 

Constraints:

1 <= squares.length <= 5 * 104
squares[i] = [xi, yi, li]
squares[i].length == 3
0 <= xi, yi <= 109
1 <= li <= 109
The total area of all the squares will not exceed 1015.



