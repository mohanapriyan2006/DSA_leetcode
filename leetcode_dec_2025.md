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





