----------------------------------
# LeetCode - ***september*** 2025
----------------------------------


# # 1792. Maximum Average Pass Ratio -> [LEETCODE](https://leetcode.com/problems/maximum-average-pass-ratio/description/)
 
Medium
 
There is a school that has classes of students and each class will be having a final exam. You are given a 2D integer array classes, where classes[i] = [passi, totali]. You know beforehand that in the ith class, there are totali total students, but only passi number of students will pass the exam.

You are also given an integer extraStudents. There are another extraStudents brilliant students that are guaranteed to pass the exam of any class they are assigned to. You want to assign each of the extraStudents students to a class in a way that maximizes the average pass ratio across all the classes.

The pass ratio of a class is equal to the number of students of the class that will pass the exam divided by the total number of students of the class. The average pass ratio is the sum of pass ratios of all the classes divided by the number of the classes.

Return the maximum possible average pass ratio after assigning the extraStudents students. Answers within 10-5 of the actual answer will be accepted.

 

Example 1:

Input: classes = [[1,2],[3,5],[2,2]], extraStudents = 2
Output: 0.78333
Explanation: You can assign the two extra students to the first class. The average pass ratio will be equal to (3/4 + 3/5 + 2/2) / 3 = 0.78333.


Example 2:

Input: classes = [[2,4],[3,9],[4,5],[2,10]], extraStudents = 4
Output: 0.53485
 

Constraints:

1 <= classes.length <= 105
classes[i].length == 2
1 <= passi <= totali <= 105
1 <= extraStudents <= 105


# Code
```cpp []
class Solution {
 public:
  double maxAverageRatio(vector<vector<int>>& classes, int extraStudents) { 
    priority_queue<tuple<double, int, int>> maxHeap;

    for (const vector<int>& c : classes) {
      const int pass = c[0];
      const int total = c[1];
      maxHeap.emplace(extraPassRatio(pass, total), pass, total);
    }

    for (int i = 0; i < extraStudents; ++i) {
      const auto [_, pass, total] = maxHeap.top();
      maxHeap.pop();
      maxHeap.emplace(extraPassRatio(pass + 1, total + 1), pass + 1, total + 1);
    }

    double ratioSum = 0;

    while (!maxHeap.empty()) {
      const auto [_, pass, total] = maxHeap.top();
      maxHeap.pop();
      ratioSum += pass / static_cast<double>(total);
    }

    return ratioSum / classes.size();
  }

 private: 
  double extraPassRatio(int pass, int total) {
    return (pass + 1) / static_cast<double>(total + 1) -
           pass / static_cast<double>(total);
  }
};
```


-----------------


# 3025. Find the Number of Ways to Place People I -> [LeetCode](https://leetcode.com/problems/find-the-number-of-ways-to-place-people-i/description)
 
Medium
 
You are given a 2D array points of size n x 2 representing integer coordinates of some points on a 2D plane, where points[i] = [xi, yi].

Count the number of pairs of points (A, B), where

A is on the upper left side of B, and
there are no other points in the rectangle (or line) they make (including the border).
Return the count.

 

Example 1:

Input: points = [[1,1],[2,2],[3,3]]

Output: 0

Explanation:

![img](https://assets.leetcode.com/uploads/2024/01/04/example1alicebob.png)

There is no way to choose A and B so A is on the upper left side of B.



Example 2:

Input: points = [[6,2],[4,4],[2,6]]

Output: 2

Explanation:

![img](https://assets.leetcode.com/uploads/2024/06/25/t2.jpg)

The left one is the pair (points[1], points[0]), where points[1] is on the upper left side of points[0] and the rectangle is empty.
The middle one is the pair (points[2], points[1]), same as the left one it is a valid pair.
The right one is the pair (points[2], points[0]), where points[2] is on the upper left side of points[0], but points[1] is inside the rectangle so it's not a valid pair.


Example 3:

Input: points = [[3,1],[1,3],[1,1]]

Output: 2

Explanation:

![img](https://assets.leetcode.com/uploads/2024/06/25/t3.jpg)

The left one is the pair (points[2], points[0]), where points[2] is on the upper left side of points[0] and there are no other points on the line they form. Note that it is a valid state when the two points form a line.
The middle one is the pair (points[1], points[2]), it is a valid pair same as the left one.
The right one is the pair (points[1], points[0]), it is not a valid pair as points[2] is on the border of the rectangle.
 

Constraints:

2 <= n <= 50
points[i].length == 2
0 <= points[i][0], points[i][1] <= 50
All points[i] are distinct.

# Code
```cpp []
class Solution {
 public:
  int numberOfPairs(vector<vector<int>>& points) {
    int ans = 0;

    ranges::sort(points, ranges::less{}, [](const vector<int>& point) {
      const int x = point[0];
      const int y = point[1];
      return pair<int, int>{x, -y};
    });

    for (int i = 0; i < points.size(); ++i) {
      int maxY = INT_MIN;
      for (int j = i + 1; j < points.size(); ++j)
        if (points[i][1] >= points[j][1] && points[j][1] > maxY) {
          ++ans;
          maxY = points[j][1];
        }
    }

    return ans;
  }
};
```

-------------------------


# 3027. Find the Number of Ways to Place People II
 
Hard

You are given a 2D array points of size n x 2 representing integer coordinates of some points on a 2D-plane, where points[i] = [xi, yi].

We define the right direction as positive x-axis (increasing x-coordinate) and the left direction as negative x-axis (decreasing x-coordinate). Similarly, we define the up direction as positive y-axis (increasing y-coordinate) and the down direction as negative y-axis (decreasing y-coordinate)

You have to place n people, including Alice and Bob, at these points such that there is exactly one person at every point. Alice wants to be alone with Bob, so Alice will build a rectangular fence with Alice's position as the upper left corner and Bob's position as the lower right corner of the fence (Note that the fence might not enclose any area, i.e. it can be a line). If any person other than Alice and Bob is either inside the fence or on the fence, Alice will be sad.

Return the number of pairs of points where you can place Alice and Bob, such that Alice does not become sad on building the fence.

Note that Alice can only build a fence with Alice's position as the upper left corner, and Bob's position as the lower right corner. For example, Alice cannot build either of the fences in the picture below with four corners (1, 1), (1, 3), (3, 1), and (3, 3), because:

With Alice at (3, 3) and Bob at (1, 1), Alice's position is not the upper left corner and Bob's position is not the lower right corner of the fence.
With Alice at (1, 3) and Bob at (1, 1), Bob's position is not the lower right corner of the fence.

 

Example 1:


Input: points = [[1,1],[2,2],[3,3]]
Output: 0
Explanation: There is no way to place Alice and Bob such that Alice can build a fence with Alice's position as the upper left corner and Bob's position as the lower right corner. Hence we return 0. 



Example 2:


Input: points = [[6,2],[4,4],[2,6]]
Output: 2
Explanation: There are two ways to place Alice and Bob such that Alice will not be sad:
- Place Alice at (4, 4) and Bob at (6, 2).
- Place Alice at (2, 6) and Bob at (4, 4).
You cannot place Alice at (2, 6) and Bob at (6, 2) because the person at (4, 4) will be inside the fence.


Example 3:


Input: points = [[3,1],[1,3],[1,1]]
Output: 2
Explanation: There are two ways to place Alice and Bob such that Alice will not be sad:
- Place Alice at (1, 1) and Bob at (3, 1).
- Place Alice at (1, 3) and Bob at (1, 1).
You cannot place Alice at (1, 3) and Bob at (3, 1) because the person at (1, 1) will be on the fence.
Note that it does not matter if the fence encloses any area, the first and second fences in the image are valid.
 

Constraints:

2 <= n <= 1000
points[i].length == 2
-109 <= points[i][0], points[i][1] <= 109
All points[i] are distinct.


# Code
```cpp []
class Solution {
 public:
 
  int numberOfPairs(vector<vector<int>>& points) {
    int ans = 0;

    ranges::sort(points, ranges::less{}, [](const vector<int>& point) {
      const int x = point[0];
      const int y = point[1];
      return pair<int, int>{x, -y};
    });

    for (int i = 0; i < points.size(); ++i) {
      int maxY = INT_MIN;
      for (int j = i + 1; j < points.size(); ++j)
        if (points[i][1] >= points[j][1] && points[j][1] > maxY) {
          ++ans;
          maxY = points[j][1];
        }
    }

    return ans;
  }
};



```

--------------------
















