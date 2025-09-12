
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


# 3027. Find the Number of Ways to Place People II -> [LeetCode](https://leetcode.com/problems/find-the-number-of-ways-to-place-people-ii/description)
 
Hard

You are given a 2D array points of size n x 2 representing integer coordinates of some points on a 2D-plane, where points[i] = [xi, yi].

We define the right direction as positive x-axis (increasing x-coordinate) and the left direction as negative x-axis (decreasing x-coordinate). Similarly, we define the up direction as positive y-axis (increasing y-coordinate) and the down direction as negative y-axis (decreasing y-coordinate)

You have to place n people, including Alice and Bob, at these points such that there is exactly one person at every point. Alice wants to be alone with Bob, so Alice will build a rectangular fence with Alice's position as the upper left corner and Bob's position as the lower right corner of the fence (Note that the fence might not enclose any area, i.e. it can be a line). If any person other than Alice and Bob is either inside the fence or on the fence, Alice will be sad.

Return the number of pairs of points where you can place Alice and Bob, such that Alice does not become sad on building the fence.

Note that Alice can only build a fence with Alice's position as the upper left corner, and Bob's position as the lower right corner. For example, Alice cannot build either of the fences in the picture below with four corners (1, 1), (1, 3), (3, 1), and (3, 3), because:

With Alice at (3, 3) and Bob at (1, 1), Alice's position is not the upper left corner and Bob's position is not the lower right corner of the fence.
With Alice at (1, 3) and Bob at (1, 1), Bob's position is not the lower right corner of the fence.

![img](https://assets.leetcode.com/uploads/2024/01/04/example0alicebob-1.png)
 

Example 1:


Input: points = [[1,1],[2,2],[3,3]]
Output: 0
Explanation: There is no way to place Alice and Bob such that Alice can build a fence with Alice's position as the upper left corner and Bob's position as the lower right corner. Hence we return 0. 

![img](https://assets.leetcode.com/uploads/2024/01/04/example1alicebob.png)

Example 2:


Input: points = [[6,2],[4,4],[2,6]]
Output: 2
Explanation: There are two ways to place Alice and Bob such that Alice will not be sad:
- Place Alice at (4, 4) and Bob at (6, 2).
- Place Alice at (2, 6) and Bob at (4, 4).
You cannot place Alice at (2, 6) and Bob at (6, 2) because the person at (4, 4) will be inside the fence.

![img](https://assets.leetcode.com/uploads/2024/02/04/example2alicebob.png)

Example 3:


Input: points = [[3,1],[1,3],[1,1]]
Output: 2
Explanation: There are two ways to place Alice and Bob such that Alice will not be sad:
- Place Alice at (1, 1) and Bob at (3, 1).
- Place Alice at (1, 3) and Bob at (1, 1).
You cannot place Alice at (1, 3) and Bob at (3, 1) because the person at (1, 1) will be on the fence.
Note that it does not matter if the fence encloses any area, the first and second fences in the image are valid.


![img](https://assets.leetcode.com/uploads/2024/02/04/example4alicebob.png)

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


# 3516. Find Closest Person -> [LeetCode](https://leetcode.com/problems/find-closest-person/description/)
 
Easy

You are given three integers x, y, and z, representing the positions of three people on a number line:

x is the position of Person 1.
y is the position of Person 2.
z is the position of Person 3, who does not move.
Both Person 1 and Person 2 move toward Person 3 at the same speed.

Determine which person reaches Person 3 first:

Return 1 if Person 1 arrives first.
Return 2 if Person 2 arrives first.
Return 0 if both arrive at the same time.
Return the result accordingly.

 

Example 1:

Input: x = 2, y = 7, z = 4

Output: 1

Explanation:

Person 1 is at position 2 and can reach Person 3 (at position 4) in 2 steps.
Person 2 is at position 7 and can reach Person 3 in 3 steps.
Since Person 1 reaches Person 3 first, the output is 1.


Example 2:

Input: x = 2, y = 5, z = 6

Output: 2

Explanation:

Person 1 is at position 2 and can reach Person 3 (at position 6) in 4 steps.
Person 2 is at position 5 and can reach Person 3 in 1 step.
Since Person 2 reaches Person 3 first, the output is 2.


Example 3:

Input: x = 1, y = 5, z = 3

Output: 0

Explanation:

Person 1 is at position 1 and can reach Person 3 (at position 3) in 2 steps.
Person 2 is at position 5 and can reach Person 3 in 2 steps.
Since both Person 1 and Person 2 reach Person 3 at the same time, the output is 0.

 

Constraints:

1 <= x, y, z <= 100


# Code
```cpp []
class Solution {
public:
    int findClosest(int x, int y, int z) {
        int p1 = abs(z-x);
        int p2 = abs(z-y);
        if(p1 < p2) return 1;
        if(p1 > p2) return 2;
        return 0;
    }
};
```

---------------------


# 2749. Minimum Operations to Make the Integer Zero -> [LeetCode](https://leetcode.com/problems/minimum-operations-to-make-the-integer-zero/description)
 
Medium
 
You are given two integers num1 and num2.

In one operation, you can choose integer i in the range [0, 60] and subtract 2i + num2 from num1.

Return the integer denoting the minimum number of operations needed to make num1 equal to 0.

If it is impossible to make num1 equal to 0, return -1.

 

Example 1:

Input: num1 = 3, num2 = -2

Output: 3

Explanation: We can make 3 equal to 0 with the following operations:
- We choose i = 2 and subtract 22 + (-2) from 3, 3 - (4 + (-2)) = 1.
- We choose i = 2 and subtract 22 + (-2) from 1, 1 - (4 + (-2)) = -1.
- We choose i = 0 and subtract 20 + (-2) from -1, (-1) - (1 + (-2)) = 0.
It can be proven, that 3 is the minimum number of operations that we need to perform.


Example 2:

Input: num1 = 5, num2 = 7

Output: -1

Explanation: It can be proven, that it is impossible to make 5 equal to 0 with the given operation.

 

Constraints:

1 <= num1 <= 109
-109 <= num2 <= 109


# Code
```cpp []
class Solution {
 public:
  int makeTheIntegerZero(int num1, int num2) {
    for (long ops = 0; ops <= 60; ++ops) {
      const long target = num1 - ops * num2;
      if (__builtin_popcountl(target) <= ops && ops <= target)
        return ops;
    }

    return -1;
  }
};
```


----------------------------------


# 3495. Minimum Operations to Make Array Elements Zero -> [Leetcode](https://leetcode.com/problems/minimum-operations-to-make-array-elements-zero/description/)
 
Hard

You are given a 2D array queries, where queries[i] is of the form [l, r]. Each queries[i] defines an array of integers nums consisting of elements ranging from l to r, both inclusive.

In one operation, you can:

Select two integers a and b from the array.
Replace them with floor(a / 4) and floor(b / 4).
Your task is to determine the minimum number of operations required to reduce all elements of the array to zero for each query. Return the sum of the results for all queries.

 

Example 1:

Input: queries = [[1,2],[2,4]]

Output: 3

Explanation:

For queries[0]:

The initial array is nums = [1, 2].
In the first operation, select nums[0] and nums[1]. The array becomes [0, 0].
The minimum number of operations required is 1.
For queries[1]:

The initial array is nums = [2, 3, 4].
In the first operation, select nums[0] and nums[2]. The array becomes [0, 3, 1].
In the second operation, select nums[1] and nums[2]. The array becomes [0, 0, 0].
The minimum number of operations required is 2.
The output is 1 + 2 = 3.

Example 2:

Input: queries = [[2,6]]

Output: 4

Explanation:

For queries[0]:

The initial array is nums = [2, 3, 4, 5, 6].
In the first operation, select nums[0] and nums[3]. The array becomes [0, 3, 4, 1, 6].
In the second operation, select nums[2] and nums[4]. The array becomes [0, 3, 1, 1, 1].
In the third operation, select nums[1] and nums[2]. The array becomes [0, 0, 0, 1, 1].
In the fourth operation, select nums[3] and nums[4]. The array becomes [0, 0, 0, 0, 0].
The minimum number of operations required is 4.
The output is 4.

 

Constraints:

1 <= queries.length <= 105
queries[i].length == 2
queries[i] == [l, r]
1 <= l < r <= 109


# Code

```cpp []
class Solution {
public:
    long long expSum4[18]={1};
    long long expSum(unsigned x){
        if (x==0) return 0;
        int log4=(31-countl_zero(x))/2;
        int r=x-(1<<(2*log4));
        return expSum4[log4]+r*(log4+1LL);
    }
    long long minOperations(vector<vector<int>>& queries) {
        for(int i=1; i<18; i++){
            expSum4[i]=expSum4[i-1]+3LL*i*(1LL<<(2*(i-1)))+1;
       
        }
        long long op=0;
        for(auto& q: queries){
            int l=q[0]-1, r=q[1];
            op+=(expSum(r)-expSum(l)+1)/2;
        }
        return op;
    }
};
```

-----------------------------------------------------


# 1304. Find N Unique Integers Sum up to Zero -> [LeetCode](https://leetcode.com/problems/find-n-unique-integers-sum-up-to-zero/description/)
 
Easy
 
Given an integer n, return any array containing n unique integers such that they add up to 0.

 

Example 1:

Input: n = 5

Output: [-7,-1,1,3,4]

Explanation: These arrays also are accepted [-5,-1,1,2,3] , [-3,-1,2,-2,4].


Example 2:

Input: n = 3

Output: [-1,0,1]


Example 3:

Input: n = 1

Output: [0]
 

Constraints:

1 <= n <= 1000



# Code
```cpp []
class Solution {
public:
    vector<int> sumZero(int n) {
        vector<int> res(n);
        res[0] = n * (1 - n) / 2;
        for (int i = 1; i < n; ++i)
            res[i] = i;
        return res;
    }
};
```

------------------------------


# 1317. Convert Integer to the Sum of Two No-Zero Integers -> [LeetCode](https://leetcode.com/problems/convert-integer-to-the-sum-of-two-no-zero-integers/description/)
 
Easy
 
No-Zero integer is a positive integer that does not contain any 0 in its decimal representation.

Given an integer n, return a list of two integers [a, b] where:

a and b are No-Zero integers.
a + b = n
The test cases are generated so that there is at least one valid solution. If there are many valid solutions, you can return any of them.

 

Example 1:

Input: n = 2

Output: [1,1]

Explanation: Let a = 1 and b = 1.
Both a and b are no-zero integers, and a + b = 2 = n.


Example 2:

Input: n = 11

Output: [2,9]

Explanation: Let a = 2 and b = 9.
Both a and b are no-zero integers, and a + b = 11 = n.
Note that there are other valid answers as [8, 3] that can be accepted.
 

Constraints:

2 <= n <= 104


# Code
```cpp []
class Solution {
public:
    vector<int> getNoZeroIntegers(int n) {
        auto check = [](int num){
            while(num > 0){
                if(num % 10 == 0) return false;
                num /= 10;
            }
            return true;
        };

        for(int i=1 ; i<n ; ++i){
            int j = n - i;
            if(check(i) && check(j)) return {i,j};
        }

        return {};
    }
};
```

---------------------------------------------


# 2327. Number of People Aware of a Secret -> [LeetCode](https://leetcode.com/problems/number-of-people-aware-of-a-secret/description)
 
Medium
 
On day 1, one person discovers a secret.

You are given an integer delay, which means that each person will share the secret with a new person every day, starting from delay days after discovering the secret. You are also given an integer forget, which means that each person will forget the secret forget days after discovering it. A person cannot share the secret on the same day they forgot it, or on any day afterwards.

Given an integer n, return the number of people who know the secret at the end of day n. Since the answer may be very large, return it modulo 109 + 7.

 

Example 1:

Input: n = 6, delay = 2, forget = 4

Output: 5

Explanation:

Day 1: Suppose the first person is named A. (1 person)
Day 2: A is the only person who knows the secret. (1 person)
Day 3: A shares the secret with a new person, B. (2 people)
Day 4: A shares the secret with a new person, C. (3 people)
Day 5: A forgets the secret, and B shares the secret with a new person, D. (3 people)
Day 6: B shares the secret with E, and C shares the secret with F. (5 people)


Example 2:

Input: n = 4, delay = 1, forget = 3

Output: 6

Explanation:

Day 1: The first person is named A. (1 person)
Day 2: A shares the secret with B. (2 people)
Day 3: A and B share the secret with 2 new people, C and D. (4 people)
Day 4: A forgets the secret. B, C, and D share the secret with 3 new people. (6 people)
 


Constraints:

2 <= n <= 1000
1 <= delay < forget <= n



# Code
```cpp []
class Solution {
public:
    int peopleAwareOfSecret(int n, int delay, int forget) {
        vector<long long> dp(n + 1, 0);
        dp[1] = 1;
        long long share = 0, MOD = 1000000007;
        for (int t = 2; t <= n; t++) {
            if (t - delay > 0)
                share = (share + dp[t - delay] + MOD) % MOD;
            if (t - forget > 0)
                share = (share - dp[t - forget] + MOD) % MOD;
            dp[t] = share;
        }
        long long know = 0;
        for (int i = n - forget + 1; i <= n; i++)
            know = (know + dp[i]) % MOD;
        return (int)know;
    }
};
```

-----------------------------------------------------------

# 1733. Minimum Number of People to Teach -> [LeetCode](https://leetcode.com/problems/minimum-number-of-people-to-teach/description)
 
Medium

On a social network consisting of m users and some friendships between users, two users can communicate with each other if they know a common language.

You are given an integer n, an array languages, and an array friendships where:

There are n languages numbered 1 through n,
languages[i] is the set of languages the i​​​​​​th​​​​ user knows, and
friendships[i] = [u​​​​​​i​​​, v​​​​​​i] denotes a friendship between the users u​​​​​​​​​​​i​​​​​ and vi.
You can choose one language and teach it to some users so that all friends can communicate with each other. Return the minimum number of users you need to teach.

Note that friendships are not transitive, meaning if x is a friend of y and y is a friend of z, this doesn't guarantee that x is a friend of z.
 

Example 1:

Input: n = 2, languages = [[1],[2],[1,2]], friendships = [[1,2],[1,3],[2,3]]

Output: 1

Explanation: You can either teach user 1 the second language or user 2 the first language.


Example 2:

Input: n = 3, languages = [[2],[1,3],[1,2],[3]], friendships = [[1,4],[1,2],[3,4],[2,3]]

Output: 2

Explanation: Teach the third language to users 1 and 3, yielding two users to teach.
 

Constraints:

2 <= n <= 500
languages.length == m
1 <= m <= 500
1 <= languages[i].length <= n
1 <= languages[i][j] <= n
1 <= u​​​​​​i < v​​​​​​i <= languages.length
1 <= friendships.length <= 500
All tuples (u​​​​​i, v​​​​​​i) are unique
languages[i] contains only unique values


# Code

```cpp []
// use unordered_set for comparison
class Solution {
public:
    static bool intersection(unordered_set<int>& X, unordered_set<int>& Y){
        if (X.size()>Y.size()) return intersection(Y, X);
        for(int x: X){
            if (Y.count(x)) return 1;
        }
        return 0;
    }
    static int minimumTeachings(int n, vector<vector<int>>& languages, vector<vector<int>>& friendships) {
        int m=languages.size(); // number of people

        // store known languages for each person
        vector<unordered_set<int>> know(m);
        for (int i=0; i<m; i++) 
            for (int l : languages[i]) know[i].insert(l);
        

        // people need be taught
        unordered_set<int> need;
        need.reserve(500);
        for (auto& f : friendships) {
            int a=f[0]-1, b=f[1]-1;
            if (intersection(know[a],know[b])) continue; // can talk
            need.insert(a);
            need.insert(b);
        }

        // if no need
        if (need.size()==0) return 0;

        int ans=INT_MAX;
        for (int lang=1; lang<=n; lang++) {   // languages for 1..n
            int cnt=0;
            for (int i: need) {
                if (!know[i].count(lang)) cnt++;
            }
            ans=min(ans, cnt);
        }

        return ans;
    }
};
```

---------------------------------------------



# 2785. Sort Vowels in a String -> [LeetCode](https://leetcode.com/problems/sort-vowels-in-a-string/description)
 
Medium
 
Given a 0-indexed string s, permute s to get a new string t such that:

All consonants remain in their original places. More formally, if there is an index i with 0 <= i < s.length such that s[i] is a consonant, then t[i] = s[i].
The vowels must be sorted in the nondecreasing order of their ASCII values. More formally, for pairs of indices i, j with 0 <= i < j < s.length such that s[i] and s[j] are vowels, then t[i] must not have a higher ASCII value than t[j].
Return the resulting string.

The vowels are 'a', 'e', 'i', 'o', and 'u', and they can appear in lowercase or uppercase. Consonants comprise all letters that are not vowels.

 

Example 1:

Input: s = "lEetcOde"

Output: "lEOtcede"

Explanation: 'E', 'O', and 'e' are the vowels in s; 'l', 't', 'c', and 'd' are all consonants. The vowels are sorted according to their ASCII values, and the consonants remain in the same places.


Example 2:

Input: s = "lYmpH"

Output: "lYmpH"

Explanation: There are no vowels in s (all characters in s are consonants), so we return "lYmpH".
 

Constraints:

1 <= s.length <= 105
s consists only of letters of the English alphabet in uppercase and lowercase.


# Code
```cpp []
class Solution {
public:
    bool isVowel(char ch){
        if(ch=='a' || ch=='e' || ch=='i' || ch=='o' || ch=='u' ||
        ch=='A' || ch=='E' || ch=='I' || ch=='O' || ch=='U')return true;

        return false;
    }
    string sortVowels(string s) {
        int freq[128]={0};

        for(int i=0;i<s.size();i++){
            if(isVowel(s[i]))freq[(int)s[i]]++;
        }

        int idx=0;
        for(int i=0;i<s.size();i++){
            if(isVowel(s[i])){
                while(freq[idx]==0)idx++;
                s[i]=(char)idx;
                freq[idx]--;
            }
        }

        return s;
    }
};
```

---------------------------------------------------------------------

# 3227. Vowels Game in a String
 
Medium

Alice and Bob are playing a game on a string.

You are given a string s, Alice and Bob will take turns playing the following game where Alice starts first:

On Alice's turn, she has to remove any non-empty substring from s that contains an odd number of vowels.
On Bob's turn, he has to remove any non-empty substring from s that contains an even number of vowels.
The first player who cannot make a move on their turn loses the game. We assume that both Alice and Bob play optimally.

Return true if Alice wins the game, and false otherwise.

The English vowels are: a, e, i, o, and u.

 

Example 1:

Input: s = "leetcoder"

Output: true

Explanation:
Alice can win the game as follows:

Alice plays first, she can delete the underlined substring in s = "leetcoder" which contains 3 vowels. The resulting string is s = "der".
Bob plays second, he can delete the underlined substring in s = "der" which contains 0 vowels. The resulting string is s = "er".
Alice plays third, she can delete the whole string s = "er" which contains 1 vowel.
Bob plays fourth, since the string is empty, there is no valid play for Bob. So Alice wins the game.



Example 2:

Input: s = "bbcd"

Output: false

Explanation:
There is no valid play for Alice in her first turn, so Alice loses the game.

 

Constraints:

1 <= s.length <= 105
s consists only of lowercase English letters.


# Code
```cpp []
class Solution {
public:
    bool doesAliceWin(string s) {
        for(const char c:s){
            if(c == 'a' || c == 'e' || c == 'i' || c == 'o' || c == 'u') return true;
        }
        return false;
    }
};
```


-------------------------------------------------------------------------




