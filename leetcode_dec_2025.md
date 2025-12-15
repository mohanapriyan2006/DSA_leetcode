------------------------------------------------------------------------------
# **Leetcode** DEC - 2025 problems
------------------------------------------------------------------------------

# 2141. Maximum Running Time of N Computers -> [LeetCode](https://leetcode.com/problems/maximum-running-time-of-n-computers/description)
 
Hard
 
You have n computers. You are given the integer n and a 0-indexed integer array batteries where the ith battery can run a computer for batteries[i] minutes. You are interested in running all n computers simultaneously using the given batteries.

Initially, you can insert at most one battery into each computer. After that and at any integer time moment, you can remove a battery from a computer and insert another battery any number of times. The inserted battery can be a totally new battery or a battery from another computer. You may assume that the removing and inserting processes take no time.

Note that the batteries cannot be recharged.

Return the maximum number of minutes you can run all the n computers simultaneously.

 

Example 1:


Input: n = 2, batteries = [3,3,3]

Output: 4

![img](https://assets.leetcode.com/uploads/2022/01/06/example1-fit.png)

Explanation: 
Initially, insert battery 0 into the first computer and battery 1 into the second computer.
After two minutes, remove battery 1 from the second computer and insert battery 2 instead. Note that battery 1 can still run for one minute.
At the end of the third minute, battery 0 is drained, and you need to remove it from the first computer and insert battery 1 instead.
By the end of the fourth minute, battery 1 is also drained, and the first computer is no longer running.
We can run the two computers simultaneously for at most 4 minutes, so we return 4.



Example 2:


Input: n = 2, batteries = [1,1,1,1]

Output: 2

![img](https://assets.leetcode.com/uploads/2022/01/06/example2.png)

Explanation: 
Initially, insert battery 0 into the first computer and battery 2 into the second computer. 
After one minute, battery 0 and battery 2 are drained so you need to remove them and insert battery 1 into the first computer and battery 3 into the second computer. 
After another minute, battery 1 and battery 3 are also drained so the first and second computers are no longer running.
We can run the two computers simultaneously for at most 2 minutes, so we return 2.
 

Constraints:

1 <= n <= batteries.length <= 105
1 <= batteries[i] <= 109

# Code
```cpp []
class Solution {
public:
    long long maxRunTime(int n, vector<int>& arr) {
        sort(arr.begin(), arr.end());
        long long total = accumulate(arr.begin(), arr.end(), 0LL);

        for (int i = arr.size() - 1; i >= 0; i--) {
            if (arr[i] <= total / n) break;
            total -= arr[i];
            n--;
        }

        return total / n;
    }
};

```


----------------------------------------------------------------------

# 3623. Count Number of Trapezoids I -> [LeetCode](https://leetcode.com/problems/count-number-of-trapezoids-i/description)

Medium
 
You are given a 2D integer array points, where points[i] = [xi, yi] represents the coordinates of the ith point on the Cartesian plane.

A horizontal trapezoid is a convex quadrilateral with at least one pair of horizontal sides (i.e. parallel to the x-axis). Two lines are parallel if and only if they have the same slope.

Return the number of unique horizontal trapezoids that can be formed by choosing any four distinct points from points.

Since the answer may be very large, return it modulo 109 + 7.

 

Example 1:

Input: points = [[1,0],[2,0],[3,0],[2,2],[3,2]]

Output: 3

Explanation:

![img](https://assets.leetcode.com/uploads/2025/05/01/desmos-graph-7.png)


There are three distinct ways to pick four points that form a horizontal trapezoid:

Using points [1,0], [2,0], [3,2], and [2,2].
Using points [2,0], [3,0], [3,2], and [2,2].
Using points [1,0], [3,0], [3,2], and [2,2].



Example 2:

Input: points = [[0,0],[1,0],[0,1],[2,1]]

Output: 1

Explanation:

![img](https://assets.leetcode.com/uploads/2025/04/29/desmos-graph-5.png)

There is only one horizontal trapezoid that can be formed.

 
Constraints:

4 <= points.length <= 105
–108 <= xi, yi <= 108
All points are pairwise distinct.



# Code
```cpp []
class Solution {
public:
    int countTrapezoids(vector<vector<int>>& points) {
        int MOD = 1000000007;
        unordered_map<int, long long> groups;
        for (auto& point : points)
            groups[point[1]]++;
        long long res = 0, total = 0;
        for (auto& group : groups){
            long long lines = group.second * (group.second - 1) / 2;
            res = (res + total * lines) % MOD;
            total = (total + lines) % MOD;
        }
        return (int)res;
    }
};
```

--------------------------------------------------------------------------------------------

# 3625. Count Number of Trapezoids II -> [LeetCode](https://leetcode.com/problems/count-number-of-trapezoids-ii/description)

Hard

You are given a 2D integer array points where points[i] = [xi, yi] represents the coordinates of the ith point on the Cartesian plane.

Return the number of unique trapezoids that can be formed by choosing any four distinct points from points.

A trapezoid is a convex quadrilateral with at least one pair of parallel sides. Two lines are parallel if and only if they have the same slope.

 

Example 1:

Input: points = [[-3,2],[3,0],[2,3],[3,2],[2,-3]]

Output: 2

Explanation:

![img](https://assets.leetcode.com/uploads/2025/04/29/desmos-graph-3.png)

There are two distinct ways to pick four points that form a trapezoid:

The points [-3,2], [2,3], [3,2], [2,-3] form one trapezoid.
The points [2,3], [3,2], [3,0], [2,-3] form another trapezoid.



Example 2:

Input: points = [[0,0],[1,0],[0,1],[2,1]]

Output: 1

Explanation:

![img](https://assets.leetcode.com/uploads/2025/04/29/desmos-graph-5.png)

There is only one trapezoid which can be formed.

 

Constraints:

4 <= points.length <= 500
–1000 <= xi, yi <= 1000
All points are pairwise distinct.




# Code
```cpp []
constexpr int bias=1<<11;
class Solution {
public:
    using ll=long long;

    // Pack 2 integers into one  key
    static int pack2(int a, int b) {
        return ((ll)(a+bias)<<16) | (b+bias);
    }

    // Pack 3 integers into one 64-bit key, note |c|<=2e6
    static ll pack3(int a, int b, int c) {
        return ((ll)(a+bias)<<50)|((ll)(b+bias)<<30)|(c+bias*bias);
    }

    // Pack 4 integers into one 64-bit key
    static ll pack4(int a, int b, int c, int d) {
        return ((ll)(a+bias)<<48)|((ll)(b+bias)<<32)|((ll)(c+bias)<<16)|(d+ bias);
    }

    static int countTrapezoids(vector<vector<int>>& points) {
        const int n=points.size();
        const int nn=n*(n-1);

        unordered_map<ll,int> coeff, midPointWslope;
        unordered_map<ll,int> slope, midPoint;

        coeff.reserve(nn);
        slope.reserve(nn);
        midPointWslope.reserve(nn);
        midPoint.reserve(nn);

        int cnt=0;

        for(int i=0; i<n-1; i++) {
            const int x0=points[i][0], y0=points[i][1];
            for(int j=i+1; j< n; j++) {
                const int x1=points[j][0], y1=points[j][1];
                
                int a=y1-y0;
                int b=x0-x1;
                int c=y0*x1-y1*x0;

                if(a==0 && b<0) { b=-b; c=-c; }
                else if(a<0) { a=-a; b=-b; c=-c; }

                int gm=gcd(a, b), gc=gcd(gm, c);

                int ab=pack2(a/gm, b/gm);           
                ll abc=pack3(a/gc, b/gc, c/gc);    

                ll midP=pack2(x0+x1, y0+y1);       
                ll midab=pack4(x0+x1, y0+y1, a/gm, b/gm); 

                cnt+=(slope[ab]++)
                    -(coeff[abc]++)
                    -(midPoint[midP]++)
                    +(midPointWslope[midab]++);
            }
        }
        return cnt;
    }
};
```

--------------------------------------------------------------------------------------------------

# 2211. Count Collisions on a Road -> [LeetCode](https://leetcode.com/problems/count-collisions-on-a-road/description)

Medium
 
There are n cars on an infinitely long road. The cars are numbered from 0 to n - 1 from left to right and each car is present at a unique point.

You are given a 0-indexed string directions of length n. directions[i] can be either 'L', 'R', or 'S' denoting whether the ith car is moving towards the left, towards the right, or staying at its current point respectively. Each moving car has the same speed.

The number of collisions can be calculated as follows:

When two cars moving in opposite directions collide with each other, the number of collisions increases by 2.
When a moving car collides with a stationary car, the number of collisions increases by 1.
After a collision, the cars involved can no longer move and will stay at the point where they collided. Other than that, cars cannot change their state or direction of motion.

Return the total number of collisions that will happen on the road.

 

Example 1:

Input: directions = "RLRSLL"

Output: 5

Explanation:

The collisions that will happen on the road are:
- Cars 0 and 1 will collide with each other. Since they are moving in opposite directions, the number of collisions becomes 0 + 2 = 2.
- Cars 2 and 3 will collide with each other. Since car 3 is stationary, the number of collisions becomes 2 + 1 = 3.
- Cars 3 and 4 will collide with each other. Since car 3 is stationary, the number of collisions becomes 3 + 1 = 4.
- Cars 4 and 5 will collide with each other. After car 4 collides with car 3, it will stay at the point of collision and get hit by car 5. The number of collisions becomes 4 + 1 = 5.
Thus, the total number of collisions that will happen on the road is 5. 



Example 2:

Input: directions = "LLRR"

Output: 0

Explanation:

No cars will collide with each other. Thus, the total number of collisions that will happen on the road is 0.
 

Constraints:

1 <= directions.length <= 105
directions[i] is either 'L', 'R', or 'S'.



# Code
```cpp []
class Solution {
public:
    static int countCollisions(string& D) {
        int n=D.size();
        if (n==1) return 0;
        int l=0, r=n-1;
        while (D[l]=='L') l++;
        while (l<r && D[r]=='R') r--;
        if (l>=r) return 0;
        int col=0;
        for( ; l<=r; l++){
           col+=D[l]!='S';
        }
        return col;      
    }
};
```

--------------------------------------------------------------------------------------------

# 3432. Count Partitions with Even Sum Difference -> [LeetCode](https://leetcode.com/problems/count-partitions-with-even-sum-difference)
 
Easy

You are given an integer array nums of length n.

A partition is defined as an index i where 0 <= i < n - 1, splitting the array into two non-empty subarrays such that:

Left subarray contains indices [0, i].
Right subarray contains indices [i + 1, n - 1].
Return the number of partitions where the difference between the sum of the left and right subarrays is even.

 

Example 1:

Input: nums = [10,10,3,7,6]

Output: 4

Explanation:

The 4 partitions are:

[10], [10, 3, 7, 6] with a sum difference of 10 - 26 = -16, which is even.
[10, 10], [3, 7, 6] with a sum difference of 20 - 16 = 4, which is even.
[10, 10, 3], [7, 6] with a sum difference of 23 - 13 = 10, which is even.
[10, 10, 3, 7], [6] with a sum difference of 30 - 6 = 24, which is even.


Example 2:

Input: nums = [1,2,2]

Output: 0

Explanation:

No partition results in an even sum difference.


Example 3:

Input: nums = [2,4,6,8]

Output: 3

Explanation:

All partitions result in an even sum difference.

 

Constraints:

2 <= n == nums.length <= 100
1 <= nums[i] <= 100


# Code
```cpp []
class Solution {
public:
    int countPartitions(vector<int>& nums) {
        int sum = accumulate(nums.begin() , nums.end() , 0);
        int res = -1;

        for(const int num:nums){
            int rem = sum - num;
            if(abs(num - rem) % 2 == 0) res++;
        }

        return (res == -1) ? 0 : res;
    }
};
```

--------------------------------------------------------------------------------------


# 3578. Count Partitions With Max-Min Difference at Most K -> [LeetCode](https://leetcode.com/problems/count-partitions-with-max-min-difference-at-most-k/)

Medium
 
You are given an integer array nums and an integer k. Your task is to partition nums into one or more non-empty contiguous segments such that in each segment, the difference between its maximum and minimum elements is at most k.

Return the total number of ways to partition nums under this condition.

Since the answer may be too large, return it modulo 109 + 7.

 

Example 1:

Input: nums = [9,4,1,3,7], k = 4

Output: 6

Explanation:

There are 6 valid partitions where the difference between the maximum and minimum elements in each segment is at most k = 4:

[[9], [4], [1], [3], [7]]
[[9], [4], [1], [3, 7]]
[[9], [4], [1, 3], [7]]
[[9], [4, 1], [3], [7]]
[[9], [4, 1], [3, 7]]
[[9], [4, 1, 3], [7]]



Example 2:

Input: nums = [3,3,4], k = 0

Output: 2

Explanation:

There are 2 valid partitions that satisfy the given conditions:

[[3], [3], [4]]
[[3, 3], [4]]
 

Constraints:

2 <= nums.length <= 5 * 104
1 <= nums[i] <= 109
0 <= k <= 109


# Code
```cpp []
class Solution {
public:
    int countPartitions(vector<int>& A, int k) {
        int n = A.size(), mod = 1e9 + 7, acc = 1;
        vector<int> dp(n + 1, 0);
        dp[0] = 1;

        deque<int> minq, maxq;
        for (int i = 0, j = 0; j < n; ++j) {
            while (!maxq.empty() && A[j] > A[maxq.back()])
                maxq.pop_back();
            maxq.push_back(j);
            while (!minq.empty() && A[j] < A[minq.back()])
                minq.pop_back();
            minq.push_back(j);
            while (A[maxq.front()] - A[minq.front()] > k) {
                acc = (acc - dp[i++] + mod) % mod;
                if (minq.front() < i)
                    minq.pop_front();
                if (maxq.front() < i)
                    maxq.pop_front();
            }

            dp[j + 1] = acc;
            acc = (acc + dp[j + 1]) % mod;
        }
        return dp[n];
    }
};
```

------------------------------------------------------------------------------------------------------------

# 1523. Count Odd Numbers in an Interval Range -> [LeetCode](https://leetcode.com/problems/count-odd-numbers-in-an-interval-range/description)

Easy

Given two non-negative integers low and high. Return the count of odd numbers between low and high (inclusive).

 

Example 1:

Input: low = 3, high = 7

Output: 3

Explanation: The odd numbers between 3 and 7 are [3,5,7].



Example 2:

Input: low = 8, high = 10

Output: 1

Explanation: The odd numbers between 8 and 10 are [9].
 

Constraints:

0 <= low <= high <= 10^9


# Code
```cpp []
class Solution {
public:
    int countOdds(int low, int high) {
        int res = 0;
        for(int i=low ; i<=high ; ++i){
            if(i % 2 == 1) res++;
        }
        return res;
    }
};
```


------------------------------------------------------------------------------------------------------------------------------------------------------

# 1925. Count Square Sum Triples -> [LeetCode](https://leetcode.com/problems/count-square-sum-triples)

Easy
 
A square triple (a,b,c) is a triple where a, b, and c are integers and a2 + b2 = c2.

Given an integer n, return the number of square triples such that 1 <= a, b, c <= n.

 

Example 1:

Input: n = 5

Output: 2

Explanation: The square triples are (3,4,5) and (4,3,5).


Example 2:

Input: n = 10

Output: 4

Explanation: The square triples are (3,4,5), (4,3,5), (6,8,10), and (8,6,10).

 

Constraints:

1 <= n <= 250



# Code
```cpp []
class Solution {
public:
    int countTriples(int n) {
        int res = 0;
        for (int u = 2; u <= sqrt(n); u++) {
            for (int v = 1; v < u; v++) {
                if (~(u - v) & 1 || gcd(u, v) != 1) continue;
                int c = u * u + v * v;
                if (c > n) continue;
                res += (n / c) << 1;
            }
        }
        return res;
    }
};

```

-----------------------------------------------------------------------------------------------------------------------


# 3583. Count Special Triplets -> [LeetCode](https://leetcode.com/problems/count-special-triplets/)

Medium
 
You are given an integer array nums.

A special triplet is defined as a triplet of indices (i, j, k) such that:

0 <= i < j < k < n, where n = nums.length
nums[i] == nums[j] * 2
nums[k] == nums[j] * 2
Return the total number of special triplets in the array.

Since the answer may be large, return it modulo 109 + 7.

 

Example 1:

Input: nums = [6,3,6]

Output: 1

Explanation:

The only special triplet is (i, j, k) = (0, 1, 2), where:

nums[0] = 6, nums[1] = 3, nums[2] = 6
nums[0] = nums[1] * 2 = 3 * 2 = 6
nums[2] = nums[1] * 2 = 3 * 2 = 6


Example 2:

Input: nums = [0,1,0,0]

Output: 1

Explanation:

The only special triplet is (i, j, k) = (0, 2, 3), where:

nums[0] = 0, nums[2] = 0, nums[3] = 0
nums[0] = nums[2] * 2 = 0 * 2 = 0
nums[3] = nums[2] * 2 = 0 * 2 = 0


Example 3:

Input: nums = [8,4,2,8,4]

Output: 2

Explanation:

There are exactly two special triplets:

(i, j, k) = (0, 1, 3)
nums[0] = 8, nums[1] = 4, nums[3] = 8
nums[0] = nums[1] * 2 = 4 * 2 = 8
nums[3] = nums[1] * 2 = 4 * 2 = 8
(i, j, k) = (1, 2, 4)
nums[1] = 4, nums[2] = 2, nums[4] = 4
nums[1] = nums[2] * 2 = 2 * 2 = 4
nums[4] = nums[2] * 2 = 2 * 2 = 4
 

Constraints:

3 <= n == nums.length <= 105
0 <= nums[i] <= 105



# Code
```cpp []
const int MOD = 1e9 + 7;
class Solution {
public:
    int specialTriplets(vector<int>& nums) {
        int n = nums.size();
        long long result = 0;
        unordered_map<int, int> r, l;
        for (int val : nums) {
            r[val]++;
        }

        for (int j = 0; j < n; ++j) {
            int mid = nums[j];
            r[mid]--; 
            int left = l[2 * mid];
            int right = r[2 * mid];
            result = (result + 1LL * left * right) % MOD;
            l[mid]++;
        }

        return result;
    }
};
```

---------------------------------------------------------------------------------------------------------------------



# 3577. Count the Number of Computer Unlocking Permutations -> [LeetCode](https://leetcode.com/problems/count-the-number-of-computer-unlocking-permutations/)

Medium

You are given an array complexity of length n.

There are n locked computers in a room with labels from 0 to n - 1, each with its own unique password. The password of the computer i has a complexity complexity[i].

The password for the computer labeled 0 is already decrypted and serves as the root. All other computers must be unlocked using it or another previously unlocked computer, following this information:

You can decrypt the password for the computer i using the password for computer j, where j is any integer less than i with a lower complexity. (i.e. j < i and complexity[j] < complexity[i])
To decrypt the password for computer i, you must have already unlocked a computer j such that j < i and complexity[j] < complexity[i].
Find the number of permutations of [0, 1, 2, ..., (n - 1)] that represent a valid order in which the computers can be unlocked, starting from computer 0 as the only initially unlocked one.

Since the answer may be large, return it modulo 109 + 7.

Note that the password for the computer with label 0 is decrypted, and not the computer with the first position in the permutation.

 

Example 1:

Input: complexity = [1,2,3]

Output: 2

Explanation:

The valid permutations are:

[0, 1, 2]
Unlock computer 0 first with root password.
Unlock computer 1 with password of computer 0 since complexity[0] < complexity[1].
Unlock computer 2 with password of computer 1 since complexity[1] < complexity[2].
[0, 2, 1]
Unlock computer 0 first with root password.
Unlock computer 2 with password of computer 0 since complexity[0] < complexity[2].
Unlock computer 1 with password of computer 0 since complexity[0] < complexity[1].




Example 2:

Input: complexity = [3,3,3,4,4,4]

Output: 0

Explanation:

There are no possible permutations which can unlock all computers.

 

Constraints:

2 <= complexity.length <= 105
1 <= complexity[i] <= 109



# code 
```cpp []
class Solution {
public:
    static const int MOD = 1000000007;

    int countPermutations(vector<int>& complexity) {
        int n = complexity.size();
        int first = complexity[0];

        for (int i = 1; i < n; i++) {
            if (complexity[i] <= first) return 0;
        }

        long long fact = 1;
        for (int i = 2; i < n; i++) {
            fact = (fact * i) % MOD;
        }

        return (int)fact;
    }
};
```


------------------------------------------------------------------------



# 3531. Count Covered Buildings -> [LeetCode](https://leetcode.com/problems/count-covered-buildings/)

Medium

You are given a positive integer n, representing an n x n city. You are also given a 2D grid buildings, where buildings[i] = [x, y] denotes a unique building located at coordinates [x, y].

A building is covered if there is at least one building in all four directions: left, right, above, and below.

Return the number of covered buildings.

 

Example 1:

![img](https://assets.leetcode.com/uploads/2025/03/04/telegram-cloud-photo-size-5-6212982906394101085-m.jpg)

Input: n = 3, buildings = [[1,2],[2,2],[3,2],[2,1],[2,3]]

Output: 1

Explanation:

Only building [2,2] is covered as it has at least one building:
above ([1,2])
below ([3,2])
left ([2,1])
right ([2,3])
Thus, the count of covered buildings is 1.



Example 2:

![img](https://assets.leetcode.com/uploads/2025/03/04/telegram-cloud-photo-size-5-6212982906394101086-m.jpg)

Input: n = 3, buildings = [[1,1],[1,2],[2,1],[2,2]]

Output: 0

Explanation:

No building has at least one building in all four directions.



Example 3:

![img](https://assets.leetcode.com/uploads/2025/03/16/telegram-cloud-photo-size-5-6248862251436067566-x.jpg)

Input: n = 5, buildings = [[1,3],[3,2],[3,3],[3,5],[5,3]]

Output: 1

Explanation:

Only building [3,3] is covered as it has at least one building:
above ([1,3])
below ([5,3])
left ([3,2])
right ([3,5])
Thus, the count of covered buildings is 1.
 

Constraints:

2 <= n <= 105
1 <= buildings.length <= 105 
buildings[i] = [x, y]
1 <= x, y <= n
All coordinates of buildings are unique.


# Code
```cpp []
class Solution {
public:
    int countCoveredBuildings(int n, vector<vector<int>>& grid, int count = 0) {
        unordered_map<int,set<int>> st1, st2;
        for (auto& p : grid) {
            st1[p[0]].insert(p[1]);
            st2[p[1]].insert(p[0]);
        }
        
        for (auto& p : grid) {
            auto& it1 = st1[p[0]];
            auto& it2 = st2[p[1]];
            auto[downy, uph] = it1.equal_range(p[1]);
            auto[downx, upx] = it2.equal_range(p[0]);
            bool up = downy != it1.begin();
            bool down = uph != it1.end();
            bool left = downx != it2.begin();
            bool right = upx != it2.end();
            if (up && down && left && right) ++count;
        }
        return count;
    }
};
```


----------------------------------------------------------------------------------------------------------------------------------------------


# 3433. Count Mentions Per User -> [LeetCode](https://leetcode.com/problems/count-mentions-per-user)

Medium

You are given an integer numberOfUsers representing the total number of users and an array events of size n x 3.

Each events[i] can be either of the following two types:

Message Event: ["MESSAGE", "timestampi", "mentions_stringi"]
This event indicates that a set of users was mentioned in a message at timestampi.
The mentions_stringi string can contain one of the following tokens:
id<number>: where <number> is an integer in range [0,numberOfUsers - 1]. There can be multiple ids separated by a single whitespace and may contain duplicates. This can mention even the offline users.
ALL: mentions all users.
HERE: mentions all online users.
Offline Event: ["OFFLINE", "timestampi", "idi"]
This event indicates that the user idi had become offline at timestampi for 60 time units. The user will automatically be online again at time timestampi + 60.
Return an array mentions where mentions[i] represents the number of mentions the user with id i has across all MESSAGE events.

All users are initially online, and if a user goes offline or comes back online, their status change is processed before handling any message event that occurs at the same timestamp.

Note that a user can be mentioned multiple times in a single message event, and each mention should be counted separately.


 

Example 1:

Input: numberOfUsers = 2, events = [["MESSAGE","10","id1 id0"],["OFFLINE","11","0"],["MESSAGE","71","HERE"]]

Output: [2,2]

Explanation:

Initially, all users are online.

At timestamp 10, id1 and id0 are mentioned. mentions = [1,1]

At timestamp 11, id0 goes offline.

At timestamp 71, id0 comes back online and "HERE" is mentioned. mentions = [2,2]



Example 2:

Input: numberOfUsers = 2, events = [["MESSAGE","10","id1 id0"],["OFFLINE","11","0"],["MESSAGE","12","ALL"]]

Output: [2,2]

Explanation:

Initially, all users are online.

At timestamp 10, id1 and id0 are mentioned. mentions = [1,1]

At timestamp 11, id0 goes offline.

At timestamp 12, "ALL" is mentioned. This includes offline users, so both id0 and id1 are mentioned. mentions = [2,2]



Example 3:

Input: numberOfUsers = 2, events = [["OFFLINE","10","0"],["MESSAGE","12","HERE"]]

Output: [0,1]

Explanation:

Initially, all users are online.

At timestamp 10, id0 goes offline.

At timestamp 12, "HERE" is mentioned. Because id0 is still offline, they will not be mentioned. mentions = [0,1]

 

Constraints:

1 <= numberOfUsers <= 100
1 <= events.length <= 100
events[i].length == 3
events[i][0] will be one of MESSAGE or OFFLINE.
1 <= int(events[i][1]) <= 105
The number of id<number> mentions in any "MESSAGE" event is between 1 and 100.
0 <= <number> <= numberOfUsers - 1
It is guaranteed that the user id referenced in the OFFLINE event is online at the time the event occurs.



# Code
```cpp []
#include<ranges>
class Solution {
public:
    vector<int> countMentions(int numberOfUsers, vector<vector<string>>& events) {
        
        ranges::sort(events, {}, [](auto& e) {
            return pair(stoi(e[1]), e[0][2]);
        });

        vector<int> ans(numberOfUsers);
        vector<int> online_t(numberOfUsers);
        for (auto& e : events) {
            int cur_t = stoi(e[1]);
            string& mention = e[2];
            if (e[0][0] == 'O') {
                online_t[stoi(mention)] = cur_t + 60;
            } else if (mention[0] == 'A') {
                for (int& v : ans) {
                    v++;
                }
            } else if (mention[0] == 'H') {
                for (int i = 0; i < numberOfUsers; i++) {
                    if (online_t[i] <= cur_t) { 
                        ans[i]++;
                    }
                }
            } else {
                for (const auto& part : mention | ranges::views::split(' ')) {
                    string s(part.begin() + 2, part.end());
                    ans[stoi(s)]++;
                }
            }
        }
        return ans;
    }
};
```


------------------------------------------------------------------------------------------------------------------------------------------------------



# 3606. Coupon Code Validator -> [LeetCode](https://leetcode.com/problems/coupon-code-validator)

Easy

You are given three arrays of length n that describe the properties of n coupons: code, businessLine, and isActive. The ith coupon has:

code[i]: a string representing the coupon identifier.
businessLine[i]: a string denoting the business category of the coupon.
isActive[i]: a boolean indicating whether the coupon is currently active.
A coupon is considered valid if all of the following conditions hold:

code[i] is non-empty and consists only of alphanumeric characters (a-z, A-Z, 0-9) and underscores (_).
businessLine[i] is one of the following four categories: "electronics", "grocery", "pharmacy", "restaurant".
isActive[i] is true.
Return an array of the codes of all valid coupons, sorted first by their businessLine in the order: "electronics", "grocery", "pharmacy", "restaurant", and then by code in lexicographical (ascending) order within each category.

 

Example 1:

Input: code = ["SAVE20","","PHARMA5","SAVE@20"], businessLine = ["restaurant","grocery","pharmacy","restaurant"], isActive = [true,true,true,true]

Output: ["PHARMA5","SAVE20"]

Explanation:

First coupon is valid.
Second coupon has empty code (invalid).
Third coupon is valid.
Fourth coupon has special character @ (invalid).



Example 2:

Input: code = ["GROCERY15","ELECTRONICS_50","DISCOUNT10"], businessLine = ["grocery","electronics","invalid"], isActive = [false,true,true]

Output: ["ELECTRONICS_50"]

Explanation:

First coupon is inactive (invalid).
Second coupon is valid.
Third coupon has invalid business line (invalid).
 

Constraints:

n == code.length == businessLine.length == isActive.length
1 <= n <= 100
0 <= code[i].length, businessLine[i].length <= 100
code[i] and businessLine[i] consist of printable ASCII characters.
isActive[i] is either true or false.



# Code
```cpp []
class Solution {
public:
    vector<string> validateCoupons(vector<string>& code, vector<string>& businessLine, vector<bool>& isActive) {
        int n = code.size();

        unordered_map<string, int> businessLineSortOrder = {
            {"electronics", 0},
            {"grocery", 1},
            {"pharmacy", 2},
            {"restaurant", 3}
        };

        vector<pair<pair<int, string>, string>> sortableCoupons;

        for (int i = 0; i < n; ++i) {
            if (!isActive[i]) continue;

            if (businessLineSortOrder.find(businessLine[i]) == businessLineSortOrder.end()) continue;

            if (code[i].empty()) continue;
            bool isCodeValid = true;
            for (char c : code[i]) {
                if (!(isalnum(c) || c == '_')) {
                    isCodeValid = false;
                    break;
                }
            }
            if (!isCodeValid) continue;

            int sortIndex = businessLineSortOrder[businessLine[i]];
            sortableCoupons.push_back({{sortIndex, code[i]}, code[i]});
        }

        sort(sortableCoupons.begin(), sortableCoupons.end());

        vector<string> sortedValidCodes;
        for (auto& entry : sortableCoupons) {
            sortedValidCodes.push_back(entry.second);
        }

        return sortedValidCodes;
    }
};
```


-----------------------------------------------------------------------------------------------------------------------------------------




# 2110. Number of Smooth Descent Periods of a Stock

Medium
 
You are given an integer array prices representing the daily price history of a stock, where prices[i] is the stock price on the ith day.

A smooth descent period of a stock consists of one or more contiguous days such that the price on each day is lower than the price on the preceding day by exactly 1. The first day of the period is exempted from this rule.

Return the number of smooth descent periods.

 

Example 1:

Input: prices = [3,2,1,4]
Output: 7
Explanation: There are 7 smooth descent periods:
[3], [2], [1], [4], [3,2], [2,1], and [3,2,1]
Note that a period with one day is a smooth descent period by the definition.


Example 2:

Input: prices = [8,6,7,7]
Output: 4
Explanation: There are 4 smooth descent periods: [8], [6], [7], and [7]
Note that [8,6] is not a smooth descent period as 8 - 6 ≠ 1.


Example 3:

Input: prices = [1]
Output: 1
Explanation: There is 1 smooth descent period: [1]
 

Constraints:

1 <= prices.length <= 105
1 <= prices[i] <= 105





