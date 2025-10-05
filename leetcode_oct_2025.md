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





