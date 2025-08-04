


---------------------------------------------------
# ***LeetCode problems - ( Aug - 2025 )***
---------------------------------------------------


# 2561. Rearranging Fruits -> [LeetCode](https://leetcode.com/problems/rearranging-fruits/description/)
 
Hard
 
You have two fruit baskets containing n fruits each. You are given two 0-indexed integer arrays basket1 and basket2 representing the cost of fruit in each basket. You want to make both baskets equal. To do so, you can use the following operation as many times as you want:

Chose two indices i and j, and swap the ith fruit of basket1 with the jth fruit of basket2.
The cost of the swap is min(basket1[i],basket2[j]).
Two baskets are considered equal if sorting them according to the fruit cost makes them exactly the same baskets.

Return the minimum cost to make both the baskets equal or -1 if impossible.

 

Example 1:

Input: basket1 = [4,2,2,2], basket2 = [1,4,1,2]
Output: 1
Explanation: Swap index 1 of basket1 with index 0 of basket2, which has cost 1. Now basket1 = [4,1,2,2] and basket2 = [2,4,1,2]. Rearranging both the arrays makes them equal.


Example 2:

Input: basket1 = [2,3,4,1], basket2 = [3,2,5,1]
Output: -1
Explanation: It can be shown that it is impossible to make both the baskets equal.
 

Constraints:

basket1.length == basket2.length
1 <= basket1.length <= 105
1 <= basket1[i],basket2[i] <= 109

# Code
```cpp []
class Solution {
 public:
  long long minCost(vector<int>& basket1, vector<int>& basket2) {
    vector<int> swapped;
    unordered_map<int, int> count;

    for (const int b : basket1)
      ++count[b];

    for (const int b : basket2)
      --count[b];

    for (const auto& [num, freq] : count) {
      if (freq % 2 != 0)
        return -1;
      for (int i = 0; i < abs(freq) / 2; ++i)
        swapped.push_back(num);
    }

    const int minNum = min(ranges::min(basket1), ranges::min(basket2));
    const auto midIt = swapped.begin() + swapped.size() / 2;
    nth_element(swapped.begin(), midIt, swapped.end());
    return accumulate(swapped.begin(), midIt, 0L, [minNum](long acc, int num) {
      return acc + min(2 * minNum, num);
    });
  }
};
```

----------


# 2106. Maximum Fruits Harvested After at Most K Steps -> [LeetCode](https://leetcode.com/problems/maximum-fruits-harvested-after-at-most-k-steps/description)
 
Hard
 
Fruits are available at some positions on an infinite x-axis. You are given a 2D integer array fruits where fruits[i] = [positioni, amounti] depicts amounti fruits at the position positioni. fruits is already sorted by positioni in ascending order, and each positioni is unique.

You are also given an integer startPos and an integer k. Initially, you are at the position startPos. From any position, you can either walk to the left or right. It takes one step to move one unit on the x-axis, and you can walk at most k steps in total. For every position you reach, you harvest all the fruits at that position, and the fruits will disappear from that position.

Return the maximum total number of fruits you can harvest.

 

Example 1:

![example1](https://assets.leetcode.com/uploads/2021/11/21/1.png)

Input: fruits = [[2,8],[6,3],[8,6]], startPos = 5, k = 4
Output: 9
Explanation: 
The optimal way is to:
- Move right to position 6 and harvest 3 fruits
- Move right to position 8 and harvest 6 fruits
You moved 3 steps and harvested 3 + 6 = 9 fruits in total.


Example 2:

![example1](https://assets.leetcode.com/uploads/2021/11/21/2.png)

Input: fruits = [[0,9],[4,1],[5,7],[6,2],[7,4],[10,9]], startPos = 5, k = 4
Output: 14
Explanation: 
You can move at most k = 4 steps, so you cannot reach position 0 nor 10.
The optimal way is to:
- Harvest the 7 fruits at the starting position 5
- Move left to position 4 and harvest 1 fruit
- Move right to position 6 and harvest 2 fruits
- Move right to position 7 and harvest 4 fruits
You moved 1 + 3 = 4 steps and harvested 7 + 1 + 2 + 4 = 14 fruits in total.


Example 3:


Input: fruits = [[0,3],[6,4],[8,5]], startPos = 3, k = 2
Output: 0
Explanation:
You can move at most k = 2 steps and cannot reach any position with fruits.
 

Constraints:

1 <= fruits.length <= 105
fruits[i].length == 2
0 <= startPos, positioni <= 2 * 105
positioni-1 < positioni for any i > 0 (0-indexed)
1 <= amounti <= 104
0 <= k <= 2 * 105

# Code
```cpp []
class Solution {
 public:
  int maxTotalFruits(vector<vector<int>>& fruits, int startPos, int k) {
    const int maxRight = max(startPos, fruits.back()[0]);
    int ans = 0;
    vector<int> amounts(1 + maxRight);
    vector<int> prefix(2 + maxRight);

    for (const vector<int>& f : fruits)
      amounts[f[0]] = f[1];

    partial_sum(amounts.begin(), amounts.end(), prefix.begin() + 1);

    auto getFruits = [&](int leftSteps, int rightSteps) {
      const int l = max(0, startPos - leftSteps);
      const int r = min(maxRight, startPos + rightSteps);
      return prefix[r + 1] - prefix[l];
    };

    // Go right first.
    const int maxRightSteps = min(maxRight - startPos, k);
    for (int rightSteps = 0; rightSteps <= maxRightSteps; ++rightSteps) {
      const int leftSteps = max(0, k - 2 * rightSteps);  // Turn left
      ans = max(ans, getFruits(leftSteps, rightSteps));
    }

    // Go left first.
    const int maxLeftSteps = min(startPos, k);
    for (int leftSteps = 0; leftSteps <= maxLeftSteps; ++leftSteps) {
      const int rightSteps = max(0, k - 2 * leftSteps);  // Turn right
      ans = max(ans, getFruits(leftSteps, rightSteps));
    }

    return ans;
  }
};
```

----------------


# 904. Fruit Into Baskets -> [LeetCode](https://leetcode.com/problems/fruit-into-baskets/description)
 
Medium

You are visiting a farm that has a single row of fruit trees arranged from left to right. The trees are represented by an integer array fruits where fruits[i] is the type of fruit the ith tree produces.

You want to collect as much fruit as possible. However, the owner has some strict rules that you must follow:

You only have two baskets, and each basket can only hold a single type of fruit. There is no limit on the amount of fruit each basket can hold.
Starting from any tree of your choice, you must pick exactly one fruit from every tree (including the start tree) while moving to the right. The picked fruits must fit in one of your baskets.
Once you reach a tree with fruit that cannot fit in your baskets, you must stop.
Given the integer array fruits, return the maximum number of fruits you can pick.

 

Example 1:

Input: fruits = [1,2,1]
Output: 3
Explanation: We can pick from all 3 trees.


Example 2:

Input: fruits = [0,1,2,2]
Output: 3
Explanation: We can pick from trees [1,2,2].
If we had started at the first tree, we would only pick from trees [0,1].


Example 3:

Input: fruits = [1,2,3,2,2]
Output: 4
Explanation: We can pick from trees [2,3,2,2].
If we had started at the first tree, we would only pick from trees [1,2].
 

Constraints:

1 <= fruits.length <= 105
0 <= fruits[i] < fruits.length


# Code
```cpp []
class Solution {
 public:
  int totalFruit(vector<int>& fruits) {
    int ans = 0;
    unordered_map<int, int> count;

    for (int l = 0, r = 0; r < fruits.size(); ++r) {
      ++count[fruits[r]];
      while (count.size() > 2) {
        if (--count[fruits[l]] == 0)
          count.erase(fruits[l]);
        ++l;
      }
      ans = max(ans, r - l + 1);
    }

    return ans;
  }
};

```

---------------



