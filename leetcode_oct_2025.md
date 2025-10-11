----------------------------------------------------------------------------------------
# LeetCode problems - OCT 2025
----------------------------------------------------------------------------------------


# 407. Trapping Rain Water II -> [LeetCode](https://leetcode.com/problems/trapping-rain-water-ii/description)
 
Hard

Given an m x n integer matrix heightMap representing the height of each unit cell in a 2D elevation map, return the volume of water it can trap after raining.

 

Example 1:

![img](https://assets.leetcode.com/uploads/2021/04/08/trap1-3d.jpg)

Input: heightMap = [[1,4,3,1,3,2],[3,2,1,3,2,4],[2,3,3,2,3,1]]

Output: 4

Explanation: After the rain, water is trapped between the blocks.
We have two small ponds 1 and 3 units trapped.
The total volume of water trapped is 4.


Example 2:

![img](https://assets.leetcode.com/uploads/2021/04/08/trap2-3d.jpg)

Input: heightMap = [[3,3,3,3,3],[3,2,2,2,3],[3,2,1,2,3],[3,2,2,2,3],[3,3,3,3,3]]

Output: 10
 

Constraints:

m == heightMap.length
n == heightMap[i].length
1 <= m, n <= 200
0 <= heightMap[i][j] <= 2 * 104


# Code
```cpp []
class Solution {
public:

    int trapRainWater(vector<vector<int>>& heights) {
        int vol = 0;
        const int M = heights.size(), N = heights[0].size();
        vector<vector<bool>> visited(M, vector<bool>(N, false));
        vector<vector<int>> directions = {{0, 1}, {0, -1}, {1, 0}, {-1, 0}};
        
        auto comp = [&](const array<int, 3>& a, const array<int, 3>& b) { return a[0] >= b[0]; };
        
        // <height, row, col>
        priority_queue<array<int, 3>, vector<array<int, 3>>, decltype(comp)> min_heap(comp);
        
        // add all boundary cells
        // top and bottom cells
        for(int i = 0; i < N; i++) {
            min_heap.push({heights[0][i], 0, i}),
            min_heap.push({heights[M-1][i], M-1, i});
            visited[0][i] = true, visited[M-1][i] = true;
        }
        
        // right and left cells
        for(int i = 0; i < M; i++) {
            min_heap.push({heights[i][0], i, 0}),
            min_heap.push({heights[i][N-1], i, N-1});
            visited[i][0] = true, visited[i][N-1] = true;
        }
            
        while(!min_heap.empty()) {
            auto [height, row, col] = min_heap.top();
            min_heap.pop();
            
            // explore the neighbouring cells
            for(auto dir: directions) {
                int r = row + dir[0], c = col + dir[1];
                // process the inner cell
                if(r >= 0 && r < M && c >= 0 && c < N && !visited[r][c]) {
                    // mark current cell as visited
                    visited[r][c] = true;
                    // if current is smaller, it can store water
                    if(heights[r][c] < height)
                        vol += height - heights[r][c];
                    
                    min_heap.push({max(height, heights[r][c]), r, c});
                }
            }
        }
        return vol;
    }
};
```

--------------------------------------------------------------------------------

# 11. Container With Most Water
 
Medium
 
You are given an integer array height of length n. There are n vertical lines drawn such that the two endpoints of the ith line are (i, 0) and (i, height[i]).

Find two lines that together with the x-axis form a container, such that the container contains the most water.

Return the maximum amount of water a container can store.

Notice that you may not slant the container.

 

Example 1:

![img](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/17/question_11.jpg)

Input: height = [1,8,6,2,5,4,8,3,7]

Output: 49

Explanation: The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.


Example 2:

Input: height = [1,1]

Output: 1
 

Constraints:

n == height.length
2 <= n <= 105
0 <= height[i] <= 104


# Code
```cpp []
class Solution {
public:
    int maxArea(vector<int>& arr) {
        int ans = 0;
        int n = arr.size();
        int l = 0 , r = n - 1;

        while(l<r){
            ans = max(ans , min(arr[l] , arr[r]) * (r-l));
            if(arr[l] <= arr[r]) l++;
            else r--;
        }
       
        return ans;
    }
};
```

----------------------------------------------------------------------------------

# 417. Pacific Atlantic Water Flow -> [LeetCode](https://leetcode.com/problems/pacific-atlantic-water-flow/description)
 
Medium
 
There is an m x n rectangular island that borders both the Pacific Ocean and Atlantic Ocean. The Pacific Ocean touches the island's left and top edges, and the Atlantic Ocean touches the island's right and bottom edges.

The island is partitioned into a grid of square cells. You are given an m x n integer matrix heights where heights[r][c] represents the height above sea level of the cell at coordinate (r, c).

The island receives a lot of rain, and the rain water can flow to neighboring cells directly north, south, east, and west if the neighboring cell's height is less than or equal to the current cell's height. Water can flow from any cell adjacent to an ocean into the ocean.

Return a 2D list of grid coordinates result where result[i] = [ri, ci] denotes that rain water can flow from cell (ri, ci) to both the Pacific and Atlantic oceans.

 

Example 1:

![img](https://assets.leetcode.com/uploads/2021/06/08/waterflow-grid.jpg)


Input: heights = [[1,2,2,3,5],[3,2,3,4,4],[2,4,5,3,1],[6,7,1,4,5],[5,1,1,2,4]]

Output: [[0,4],[1,3],[1,4],[2,2],[3,0],[3,1],[4,0]]

Explanation: The following cells can flow to the Pacific and Atlantic oceans, as shown below:
[0,4]: [0,4] -> Pacific Ocean 
       [0,4] -> Atlantic Ocean
[1,3]: [1,3] -> [0,3] -> Pacific Ocean 
       [1,3] -> [1,4] -> Atlantic Ocean
[1,4]: [1,4] -> [1,3] -> [0,3] -> Pacific Ocean 
       [1,4] -> Atlantic Ocean
[2,2]: [2,2] -> [1,2] -> [0,2] -> Pacific Ocean 
       [2,2] -> [2,3] -> [2,4] -> Atlantic Ocean
[3,0]: [3,0] -> Pacific Ocean 
       [3,0] -> [4,0] -> Atlantic Ocean
[3,1]: [3,1] -> [3,0] -> Pacific Ocean 
       [3,1] -> [4,1] -> Atlantic Ocean
[4,0]: [4,0] -> Pacific Ocean 
       [4,0] -> Atlantic Ocean
Note that there are other possible paths for these cells to flow to the Pacific and Atlantic oceans.


Example 2:

Input: heights = [[1]]

Output: [[0,0]]

Explanation: The water can flow from the only cell to the Pacific and Atlantic oceans.
 

Constraints:

m == heights.length
n == heights[r].length
1 <= m, n <= 200
0 <= heights[r][c] <= 105


# Code
```cpp []
class Solution {
public:
    int m, n;
    vector<vector<int>> directions = {{1,0}, {-1,0}, {0,1}, {0,-1}};

    vector<vector<int>> pacificAtlantic(vector<vector<int>>& heights) {
        m = heights.size();
        n = heights[0].size();

        vector<vector<bool>> pacific(m, vector<bool>(n, false));
        vector<vector<bool>> atlantic(m, vector<bool>(n, false));

        for (int j = 0; j < n; j++) dfs(0, j, heights, pacific);
        for (int i = 0; i < m; i++) dfs(i, 0, heights, pacific);

        for (int j = 0; j < n; j++) dfs(m-1, j, heights, atlantic);
        for (int i = 0; i < m; i++) dfs(i, n-1, heights, atlantic);

        vector<vector<int>> result;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (pacific[i][j] && atlantic[i][j]) {
                    result.push_back({i, j});
                }
            }
        }

        return result;
    }

    void dfs(int i, int j, vector<vector<int>>& heights, vector<vector<bool>>& visited) {
        visited[i][j] = true;
        
        for (auto& d : directions) {
            int x = i + d[0], y = j + d[1];
            
            if (x < 0 || x >= m || y < 0 || y >= n) continue;
            if (visited[x][y]) continue;
            if (heights[x][y] < heights[i][j]) continue;
            
            dfs(x, y, heights, visited);
        }
    }
};
```

----------------------------------------------------------------

# 778. Swim in Rising Water -> [LeetCode](https://leetcode.com/problems/swim-in-rising-water/description/)
 
Hard
 
You are given an n x n integer matrix grid where each value grid[i][j] represents the elevation at that point (i, j).

It starts raining, and water gradually rises over time. At time t, the water level is t, meaning any cell with elevation less than equal to t is submerged or reachable.

You can swim from a square to another 4-directionally adjacent square if and only if the elevation of both squares individually are at most t. You can swim infinite distances in zero time. Of course, you must stay within the boundaries of the grid during your swim.

Return the minimum time until you can reach the bottom right square (n - 1, n - 1) if you start at the top left square (0, 0).

 

Example 1:

![img](https://assets.leetcode.com/uploads/2021/06/29/swim1-grid.jpg)

Input: grid = [[0,2],[1,3]]

Output: 3

Explanation:
At time 0, you are in grid location (0, 0).
You cannot go anywhere else because 4-directionally adjacent neighbors have a higher elevation than t = 0.
You cannot reach point (1, 1) until time 3.
When the depth of water is 3, we can swim anywhere inside the grid.


Example 2:

![img](https://assets.leetcode.com/uploads/2021/06/29/swim2-grid-1.jpg)

Input: grid = [[0,1,2,3,4],[24,23,22,21,5],[12,13,14,15,16],[11,17,18,19,20],[10,9,8,7,6]]

Output: 16

Explanation: The final route is shown.
We need to wait until time 16 so that (0, 0) and (4, 4) are connected.
 

Constraints:

n == grid.length
n == grid[i].length
1 <= n <= 50
0 <= grid[i][j] < n2
Each value grid[i][j] is unique.


# Code
```cpp []
class Disjointset
{
private:
    vector<int> parent, size; // parent will store the parents '
                              // size will be taken to rank or compare the parent order while doing union.
public:
    Disjointset(int n)
    {
        parent.resize(n + 1);
        size.resize(n, 1);
        for (int i = 0; i < n + 1; i++)
        {
            parent[i] = i; // element will be it's parent only
        }
    }
    int find(int X)
    {
        if (parent[X] == X)
            return X;

        return parent[X] = find(parent[X]); // path compression
    }
    void UNION(int X, int Y)
    {
        int parent1 = find(X);
        int parent2 = find(Y);
        if (parent1 == parent2)
            return; // CYCLE DETECTED.
        if (size[parent1] < size[parent2])
        {
            parent[parent1] = parent2;
            size[parent2] += size[parent1];
        }
        else
        {
            parent[parent2] = parent1;
            size[parent1] += size[parent2];
        }
    }
    void printArrays()
    {
        cout << "PARENT" << endl;
        for (auto it : parent)
        {
            cout << it << " ";
        }
        cout << endl;
        cout << "SIZE" << endl;
        for (auto it : size)
        {
            cout << it << " ";
        }
    }
    int SIZE(int vertex) // returns the size of the whole disjoint set of which the current vertex is a part of.
    {
        return size[find(vertex)]; // returns the size of disjoint set that it is a part of.
    }

    int noOfdisjointSets(int n) // pass n as indexing. , gives all disjoint sets and not particular
    {
        // find the parent of all nodes.

        for (int i = 0; i < n; i++)
        {
            parent[i] = find(i);
        }

        int cnt = 0;
        for (int i = 0; i < n; i++)
        {
            if (parent[i] == i)
            {
                cnt++;
            }
        }
        return cnt;

        /*
      //   METHOD 2
        set<int> s;
        for(int i=0;i<n;i++)
        {
            s.insert(parent[i]);
        }
        return s.size();
        */
    }
};

class Solution
{
public:
    int swimInWater(vector<vector<int>> &grid)
    {
        return UnionAndFind_swimInWater(grid);
    }
    int UnionAndFind_swimInWater(vector<vector<int>> &grid)
    {
        int n = grid.size();
        Disjointset ds(n * n);
        pair<int, int> locations[n * n];                // store the location of the element reachable exactly at time t.
        vector<vector<int>> vis(n, vector<int>(n, -1)); // can use grid for this purpose also.
        for (int i = 0; i < n; i++)                     // storing the locations of elements
        {
            for (int j = 0; j < n; j++)
            {
                locations[grid[i][j]] = {i, j};
            }
        }

        int delRow[] = {0, 0, 1, -1};
        int delCol[] = {1, -1, 0, 0};
        // now the time will be in range from 0 to n*n -1
        for (int time = 0; time < n * n; time++)
        {

            // find the loc of element reachable exactly at  this time {x,y}
            int x = locations[time].first;
            int y = locations[time].second;
            // mark the current as visited
            vis[x][y] = 1;
            // check if all it's neighbours, if they have already been reached then merge with it.
            for (int k = 0; k < 4; k++)
            {
                int nrow = x + delRow[k];
                int ncol = y + delCol[k];
                if (underBoundaries(nrow, ncol, n, n) && vis[nrow][ncol] == 1)
                {
                    ds.UNION(x*n+y,nrow*n+ncol);//join the locations here and not the heights.
                }
            }
            if (ds.find(0) == ds.find(n*n-1)) // if last element location in the connected component
            {
                return time;
            }
        }

        return n * n - 1; // since in max time it will be possible to reach the desired
        // the code will itself cover this situation and does not require it here only.
        /*
         some intutive improvements in the problem:
          since time is increasing linearly,
          so any element which has lesser value than current time is already visited
          so we can say element<time then already visited.
          we can save ourselves of vis extra n square space.
        */
    }
    bool underBoundaries(int nrow, int ncol, int n, int m)
    {
        if (nrow >= 0 && nrow < n && ncol >= 0 && ncol < m)
        {
            return true;
        }
        return false;
    }
};
```

-------------------------------------------------------


# 1488. Avoid Flood in The City -> [LeetCode](https://leetcode.com/problems/avoid-flood-in-the-city/description)
 
Medium
 
Your country has an infinite number of lakes. Initially, all the lakes are empty, but when it rains over the nth lake, the nth lake becomes full of water. If it rains over a lake that is full of water, there will be a flood. Your goal is to avoid floods in any lake.

Given an integer array rains where:

rains[i] > 0 means there will be rains over the rains[i] lake.
rains[i] == 0 means there are no rains this day and you can choose one lake this day and dry it.
Return an array ans where:

ans.length == rains.length
ans[i] == -1 if rains[i] > 0.
ans[i] is the lake you choose to dry in the ith day if rains[i] == 0.
If there are multiple valid answers return any of them. If it is impossible to avoid flood return an empty array.

Notice that if you chose to dry a full lake, it becomes empty, but if you chose to dry an empty lake, nothing changes.

 

Example 1:

Input: rains = [1,2,3,4]

Output: [-1,-1,-1,-1]

Explanation: After the first day full lakes are [1]
After the second day full lakes are [1,2]
After the third day full lakes are [1,2,3]
After the fourth day full lakes are [1,2,3,4]
There's no day to dry any lake and there is no flood in any lake.


Example 2:

Input: rains = [1,2,0,0,2,1]

Output: [-1,-1,2,1,-1,-1]

Explanation: After the first day full lakes are [1]
After the second day full lakes are [1,2]
After the third day, we dry lake 2. Full lakes are [1]
After the fourth day, we dry lake 1. There is no full lakes.
After the fifth day, full lakes are [2].
After the sixth day, full lakes are [1,2].
It is easy that this scenario is flood-free. [-1,-1,1,2,-1,-1] is another acceptable scenario.


Example 3:

Input: rains = [1,2,0,1,2]

Output: []

Explanation: After the second day, full lakes are  [1,2]. We have to dry one lake in the third day.
After that, it will rain over lakes [1,2]. It's easy to prove that no matter which lake you choose to dry in the 3rd day, the other one will flood.
 

Constraints:

1 <= rains.length <= 105
0 <= rains[i] <= 109


# Code
```cpp []
class UnionFind {
public:
    vector<int> parent;

    UnionFind(int size) : parent(size + 1) {
        iota(parent.begin(), parent.end(), 0);
    }

    int find(int i) {
        if (i == parent[i])
            return i;
        parent[i] = find(parent[i]);
        return parent[i];
    }

    void unite(int i) { parent[i] = find(i + 1); }
};

class Solution {
public:
    vector<int> avoidFlood(vector<int>& rain) {
        int n = rain.size();
        UnionFind uf(n + 1);
        unordered_map<int, int> map;
        vector<int> res(n, 1);

        for (int i = 0; i < n; i++) {
            int lake = rain[i];
            if (lake == 0) continue;

            res[i] = -1;
            uf.unite(i);

            if (map.find(lake) != map.end()) {
                int prev = map[lake];
                int dry = uf.find(prev + 1);

                if (dry >= i) return {};

                res[dry] = lake;
                uf.unite(dry);
                map[lake] = i;
            } else {
                map[lake] = i;
            }
        }

        return res;
    }
};
```

---------------------------------------------------------------

# 2300. Successful Pairs of Spells and Potions -> [LeetCode](https://leetcode.com/problems/successful-pairs-of-spells-and-potions/description)
 
Medium
 
You are given two positive integer arrays spells and potions, of length n and m respectively, where spells[i] represents the strength of the ith spell and potions[j] represents the strength of the jth potion.

You are also given an integer success. A spell and potion pair is considered successful if the product of their strengths is at least success.

Return an integer array pairs of length n where pairs[i] is the number of potions that will form a successful pair with the ith spell.

 

Example 1:

Input: spells = [5,1,3], potions = [1,2,3,4,5], success = 7

Output: [4,0,3]

Explanation:
- 0th spell: 5 * [1,2,3,4,5] = [5,10,15,20,25]. 4 pairs are successful.
- 1st spell: 1 * [1,2,3,4,5] = [1,2,3,4,5]. 0 pairs are successful.
- 2nd spell: 3 * [1,2,3,4,5] = [3,6,9,12,15]. 3 pairs are successful.
Thus, [4,0,3] is returned.


Example 2:

Input: spells = [3,1,2], potions = [8,5,8], success = 16

Output: [2,0,2]

Explanation:
- 0th spell: 3 * [8,5,8] = [24,15,24]. 2 pairs are successful.
- 1st spell: 1 * [8,5,8] = [8,5,8]. 0 pairs are successful. 
- 2nd spell: 2 * [8,5,8] = [16,10,16]. 2 pairs are successful. 
Thus, [2,0,2] is returned.
 

Constraints:

n == spells.length
m == potions.length
1 <= n, m <= 105
1 <= spells[i], potions[i] <= 105
1 <= success <= 1010

# Code
```cpp []
class Solution {
public:
    vector<int> successfulPairs(vector<int>& spells, vector<int>& potions, long long success) {
        int n = spells.size();
        int m = potions.size();
        vector<int> pairs(n, 0);
        sort(potions.begin(), potions.end());
        for (int i = 0; i < n; i++) {
            int spell = spells[i];
            int left = 0;
            int right = m - 1;
            while (left <= right) {
                int mid = left + (right - left) / 2;
                long long product = (long long)spell * (long long)potions[mid];
                if (product >= success) {
                    right = mid - 1;
                } else {
                    left = mid + 1;
                }
            }
            pairs[i] = m - left;
        }
        return pairs;
    }
};
```
------------------------------------------------


# 3494. Find the Minimum Amount of Time to Brew Potions -> [LeetCode](https://leetcode.com/problems/find-the-minimum-amount-of-time-to-brew-potions/description)
 
Medium
 
You are given two integer arrays, skill and mana, of length n and m, respectively.

In a laboratory, n wizards must brew m potions in order. Each potion has a mana capacity mana[j] and must pass through all the wizards sequentially to be brewed properly. The time taken by the ith wizard on the jth potion is timeij = skill[i] * mana[j].

Since the brewing process is delicate, a potion must be passed to the next wizard immediately after the current wizard completes their work. This means the timing must be synchronized so that each wizard begins working on a potion exactly when it arrives. ​

Return the minimum amount of time required for the potions to be brewed properly.

 

Example 1:

Input: skill = [1,5,2,4], mana = [5,1,4,2]

Output: 110

Explanation:

Potion Number	Start time	Wizard 0 done by	Wizard 1 done by	Wizard 2 done by	Wizard 3 done by
0	0	5	30	40	60
1	52	53	58	60	64
2	54	58	78	86	102
3	86	88	98	102	110
As an example for why wizard 0 cannot start working on the 1st potion before time t = 52, consider the case where the wizards started preparing the 1st potion at time t = 50. At time t = 58, wizard 2 is done with the 1st potion, but wizard 3 will still be working on the 0th potion till time t = 60.


Example 2:

Input: skill = [1,1,1], mana = [1,1,1]

Output: 5

Explanation:

Preparation of the 0th potion begins at time t = 0, and is completed by time t = 3.
Preparation of the 1st potion begins at time t = 1, and is completed by time t = 4.
Preparation of the 2nd potion begins at time t = 2, and is completed by time t = 5.


Example 3:

Input: skill = [1,2,3,4], mana = [1,2]

Output: 21

 

Constraints:

n == skill.length
m == mana.length
1 <= n, m <= 5000
1 <= mana[i], skill[i] <= 5000

# Code
```cpp []
class Solution {
public:
    long long minTime(vector<int>& skill, vector<int>& mana) {
    int n = skill.size(), m = mana.size();
    vector<long long> done(n + 1);
    for (int j = 0; j < m; ++j) {
        for (int i = 0; i < n; ++i)
            done[i + 1] = max(done[i + 1], done[i]) + mana[j] * skill[i];
        for (int i = n - 1; i > 0; --i)
            done[i] = done[i + 1] - mana[j] * skill[i];     
    }
    return done.back();
}
};
```

-----------------------------------------------------

# 3147. Taking Maximum Energy From the Mystic Dungeon -> [LeetCode](https://leetcode.com/problems/taking-maximum-energy-from-the-mystic-dungeon/description)
 
Medium
 
In a mystic dungeon, n magicians are standing in a line. Each magician has an attribute that gives you energy. Some magicians can give you negative energy, which means taking energy from you.

You have been cursed in such a way that after absorbing energy from magician i, you will be instantly transported to magician (i + k). This process will be repeated until you reach the magician where (i + k) does not exist.

In other words, you will choose a starting point and then teleport with k jumps until you reach the end of the magicians' sequence, absorbing all the energy during the journey.

You are given an array energy and an integer k. Return the maximum possible energy you can gain.

Note that when you are reach a magician, you must take energy from them, whether it is negative or positive energy.

 

Example 1:

Input: energy = [5,2,-10,-5,1], k = 3

Output: 3

Explanation: We can gain a total energy of 3 by starting from magician 1 absorbing 2 + 1 = 3.

Example 2:

Input: energy = [-2,-3,-1], k = 2

Output: -1

Explanation: We can gain a total energy of -1 by starting from magician 2.

 

Constraints:

1 <= energy.length <= 105
-1000 <= energy[i] <= 1000
1 <= k <= energy.length - 1


# Code
```cpp []
class Solution {
public:
    int maximumEnergy(vector<int>& energy, int k){
        int n = energy.size(), ans = INT_MIN;

        for(int j = n - k - 1; j >= 0; j--){
            energy[j] += energy[j + k];
        }

        for(int i = 0; i < n; i++){
            ans = max(ans, energy[i]);
        }
        return ans;
    }
};
```
---------------------------------------------------------------------



# Code
```cpp []
#include <vector>
#include <unordered_map>
#include <algorithm>

class Solution {
public:
    long long maximumTotalDamage(std::vector<int>& power) {
        std::unordered_map<int, long long> damageFrequency;
        for (int damage : power) {
            damageFrequency[damage]++;
        }

        std::vector<int> uniqueDamages;
        for (const auto& pair : damageFrequency) {
            uniqueDamages.push_back(pair.first);
        }
        std::sort(uniqueDamages.begin(), uniqueDamages.end());

        int totalUniqueDamages = uniqueDamages.size();
        std::vector<long long> maxDamageDP(totalUniqueDamages, 0);

        maxDamageDP[0] = uniqueDamages[0] * damageFrequency[uniqueDamages[0]];

        for (int i = 1; i < totalUniqueDamages; i++) {
            int currentDamageValue = uniqueDamages[i];
            long long currentDamageTotal = currentDamageValue * damageFrequency[currentDamageValue];

            maxDamageDP[i] = maxDamageDP[i - 1];

            int previousIndex = i - 1;
            while (previousIndex >= 0 && 
                   (uniqueDamages[previousIndex] == currentDamageValue - 1 || 
                    uniqueDamages[previousIndex] == currentDamageValue - 2 || 
                    uniqueDamages[previousIndex] == currentDamageValue + 1 || 
                    uniqueDamages[previousIndex] == currentDamageValue + 2)) {
                previousIndex--;
            }

            if (previousIndex >= 0) {
                maxDamageDP[i] = std::max(maxDamageDP[i], maxDamageDP[previousIndex] + currentDamageTotal);
            } else {
                maxDamageDP[i] = std::max(maxDamageDP[i], currentDamageTotal);
            }
        }

        return maxDamageDP[totalUniqueDamages - 1];
    }
};
```

--------------------------------------------------------------------------



