----------------------------------------------------------------------------------------
# LeetCode problems - OCT 2025
----------------------------------------------------------------------------------------


# 407. Trapping Rain Water II -> [LeetCode](https://leetcode.com/problems/trapping-rain-water-ii/description)
 
Hard

Given an m x n integer matrix heightMap representing the height of each unit cell in a 2D elevation map, return the volume of water it can trap after raining.

 

Example 1:



Input: heightMap = [[1,4,3,1,3,2],[3,2,1,3,2,4],[2,3,3,2,3,1]]

Output: 4

Explanation: After the rain, water is trapped between the blocks.
We have two small ponds 1 and 3 units trapped.
The total volume of water trapped is 4.


Example 2:

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



