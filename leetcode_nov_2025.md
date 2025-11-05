----------------------------------------------------------------------------------------
# LeetCode problems - NOV 2025
----------------------------------------------------------------------------------------


# 3217. Delete Nodes From Linked List Present in Array -> [LeetCode](https://leetcode.com/problems/delete-nodes-from-linked-list-present-in-array/description/)
 
Medium
 
You are given an array of integers nums and the head of a linked list. Return the head of the modified linked list after removing all nodes from the linked list that have a value that exists in nums.

 

Example 1:

Input: nums = [1,2,3], head = [1,2,3,4,5]

Output: [4,5]

Explanation:

![img](https://assets.leetcode.com/uploads/2024/06/11/linkedlistexample0.png)


Remove the nodes with values 1, 2, and 3.

Example 2:

Input: nums = [1], head = [1,2,1,2,1,2]

Output: [2,2,2]

Explanation:

![img](https://assets.leetcode.com/uploads/2024/06/11/linkedlistexample1.png)


Remove the nodes with value 1.

Example 3:

Input: nums = [5], head = [1,2,3,4]

Output: [1,2,3,4]

Explanation:

![img](https://assets.leetcode.com/uploads/2024/06/11/linkedlistexample2.png)


No node has value 5.

 

Constraints:

1 <= nums.length <= 105
1 <= nums[i] <= 105
All elements in nums are unique.
The number of nodes in the given list is in the range [1, 105].
1 <= Node.val <= 105
The input is generated such that there is at least one node in the linked list that has a value not present in nums.



# Code
```cpp []
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* modifiedList(vector<int>& nums, ListNode* head) {
        unordered_set<int> mpp(nums.begin(), nums.end());

        while (head && mpp.count(head->val))
            head = head->next;

        ListNode* curr = head;
        while (curr && curr->next) {
            while (curr->next && mpp.count(curr->next->val)) {
                curr->next = curr->next->next;
            }
            curr = curr->next;
        }
        return head;
    }
};
```

-----------------------------------------------------------------------------------------


# 2257. Count Unguarded Cells in the Grid -> [LeetCode](https://leetcode.com/problems/count-unguarded-cells-in-the-grid/description)
 
Medium
 
You are given two integers m and n representing a 0-indexed m x n grid. You are also given two 2D integer arrays guards and walls where guards[i] = [rowi, coli] and walls[j] = [rowj, colj] represent the positions of the ith guard and jth wall respectively.

A guard can see every cell in the four cardinal directions (north, east, south, or west) starting from their position unless obstructed by a wall or another guard. A cell is guarded if there is at least one guard that can see it.

Return the number of unoccupied cells that are not guarded.

 

Example 1:

![img](https://assets.leetcode.com/uploads/2022/03/10/example1drawio2.png)

Input: m = 4, n = 6, guards = [[0,0],[1,1],[2,3]], walls = [[0,1],[2,2],[1,4]]

Output: 7

Explanation: The guarded and unguarded cells are shown in red and green respectively in the above diagram.
There are a total of 7 unguarded cells, so we return 7.


Example 2:

![img](https://assets.leetcode.com/uploads/2022/03/10/example2drawio.png)

Input: m = 3, n = 3, guards = [[1,1]], walls = [[0,1],[1,0],[2,1],[1,2]]

Output: 4

Explanation: The unguarded cells are shown in green in the above diagram.
There are a total of 4 unguarded cells, so we return 4.
 

Constraints:

1 <= m, n <= 105
2 <= m * n <= 105
1 <= guards.length, walls.length <= 5 * 104
2 <= guards.length + walls.length <= m * n
guards[i].length == walls[j].length == 2
0 <= rowi, rowj < m
0 <= coli, colj < n
All the positions in guards and walls are unique.



# Code
```cpp []
class Solution {
public:
    int countUnguarded(int m, int n, vector<vector<int>>& guards, vector<vector<int>>& walls) {
        // Initialize grid with zeros
        int g[m][n];
        memset(g, 0, sizeof(g));
        
        // Mark guards and walls as 2
        for (auto& e : guards) {
            g[e[0]][e[1]] = 2;
        }
        for (auto& e : walls) {
            g[e[0]][e[1]] = 2;
        }
        
        // Directions: up, right, down, left
        int dirs[5] = {-1, 0, 1, 0, -1};
        
        // Process each guard's line of sight
        for (auto& e : guards) {
            for (int k = 0; k < 4; ++k) {
                int x = e[0], y = e[1];
                int dx = dirs[k], dy = dirs[k + 1];
                
                // Check cells in current direction until hitting boundary or obstacle
                while (x + dx >= 0 && x + dx < m && y + dy >= 0 && y + dy < n && g[x + dx][y + dy] < 2) {
                    x += dx;
                    y += dy;
                    g[x][y] = 1;
                }
            }
        }
        
        // Count unguarded cells (cells with value 0)
        int unguardedCount = 0;
        for (int i = 0; i < m; i++) {
            unguardedCount += count(g[i], g[i] + n, 0);
        }
        
        return unguardedCount;
    }
};
```


----------------------------------------------------------------------------------------

# 1578. Minimum Time to Make Rope Colorful -> [LeetCode](https://leetcode.com/problems/minimum-time-to-make-rope-colorful/description)
 
Medium
 
Alice has n balloons arranged on a rope. You are given a 0-indexed string colors where colors[i] is the color of the ith balloon.

Alice wants the rope to be colorful. She does not want two consecutive balloons to be of the same color, so she asks Bob for help. Bob can remove some balloons from the rope to make it colorful. You are given a 0-indexed integer array neededTime where neededTime[i] is the time (in seconds) that Bob needs to remove the ith balloon from the rope.

Return the minimum time Bob needs to make the rope colorful.

 

Example 1:

![img](https://assets.leetcode.com/uploads/2021/12/13/ballon1.jpg)

Input: colors = "abaac", neededTime = [1,2,3,4,5]

Output: 3

Explanation: In the above image, 'a' is blue, 'b' is red, and 'c' is green.
Bob can remove the blue balloon at index 2. This takes 3 seconds.
There are no longer two consecutive balloons of the same color. Total time = 3.


Example 2:

![img](https://assets.leetcode.com/uploads/2021/12/13/balloon2.jpg)

Input: colors = "abc", neededTime = [1,2,3]

Output: 0

Explanation: The rope is already colorful. Bob does not need to remove any balloons from the rope.


Example 3:

![img](https://assets.leetcode.com/uploads/2021/12/13/balloon3.jpg)

Input: colors = "aabaa", neededTime = [1,2,3,4,1]

Output: 2

Explanation: Bob will remove the balloons at indices 0 and 4. Each balloons takes 1 second to remove.
There are no longer two consecutive balloons of the same color. Total time = 1 + 1 = 2.
 

Constraints:

n == colors.length == neededTime.length
1 <= n <= 105
1 <= neededTime[i] <= 104
colors contains only lowercase English letters.


# Code
```cpp []

class Solution {
public:
    int minCost(string colors, vector<int>& neededTime) {
        int totalTime = 0; 
        int i = 0, j = 0; 

        while (i < neededTime.size() && j < neededTime.size()) {
            int currTotal = 0, currMax = 0; 

            while (j < neededTime.size() && colors[i] == colors[j]) {
                currTotal += neededTime[j];
        
                currMax = max(currMax, neededTime[j]); 
                                                       
                j++;
            }

            totalTime += currTotal - currMax; 
            i = j; 
        }
        return totalTime; 
    }
};

```

------------------------------------------------------------------------------------------


# 3318. Find X-Sum of All K-Long Subarrays I -> [LeetCode](https://leetcode.com/problems/find-x-sum-of-all-k-long-subarrays-i)
 
Easy
 
You are given an array nums of n integers and two integers k and x.

The x-sum of an array is calculated by the following procedure:

Count the occurrences of all elements in the array.
Keep only the occurrences of the top x most frequent elements. If two elements have the same number of occurrences, the element with the bigger value is considered more frequent.
Calculate the sum of the resulting array.
Note that if an array has less than x distinct elements, its x-sum is the sum of the array.

Return an integer array answer of length n - k + 1 where answer[i] is the x-sum of the subarray nums[i..i + k - 1].

 

Example 1:

Input: nums = [1,1,2,2,3,4,2,3], k = 6, x = 2

Output: [6,10,12]

Explanation:

For subarray [1, 1, 2, 2, 3, 4], only elements 1 and 2 will be kept in the resulting array. Hence, answer[0] = 1 + 1 + 2 + 2.
For subarray [1, 2, 2, 3, 4, 2], only elements 2 and 4 will be kept in the resulting array. Hence, answer[1] = 2 + 2 + 2 + 4. Note that 4 is kept in the array since it is bigger than 3 and 1 which occur the same number of times.
For subarray [2, 2, 3, 4, 2, 3], only elements 2 and 3 are kept in the resulting array. Hence, answer[2] = 2 + 2 + 2 + 3 + 3.



Example 2:

Input: nums = [3,8,7,8,7,5], k = 2, x = 2

Output: [11,15,15,15,12]

Explanation:

Since k == x, answer[i] is equal to the sum of the subarray nums[i..i + k - 1].

 

Constraints:

1 <= n == nums.length <= 50
1 <= nums[i] <= 50
1 <= x <= k <= nums.length



# Code
```cpp []
class Solution {
public:
    using int2=pair<int, int>;
    static int x_sum( const auto& freq, int k, int x){
        auto freq2=freq;
        sort(freq2.begin(), freq2.end(), greater<int2>());
        int sum=0;
        for (int i=0; i<x; i++){
            auto [f, num]=freq2[i];
            if (f==0) break;
            sum+=num*f;
        }
        return sum;
    }
    static vector<int> findXSum(vector<int>& nums, int k, int x) {
        const int n=nums.size(), sz=n-k+1;
        vector<int> ans(sz);
        array<int2, 51> freq;
        freq.fill({0, 0});
        for(int r=0; r<k; r++){
            int z=nums[r];
            freq[z].second=z;
            freq[z].first++;
        }
        ans[0]=x_sum(freq, k, x);
        for(int l=1, r=k; l<sz; l++, r++){
            int L=nums[l-1], R=nums[r];
            freq[L].first--;
            freq[R].first++;
            freq[R].second = R;
            ans[l]=x_sum(freq, k, x);
        }
        return ans;
    }
};


auto init = []() {
    ios::sync_with_stdio(0);
    cin.tie(0);
    cout.tie(0);
    return 'c';
}();
```

-----------------------------------------------------------------------------------------


# 3321. Find X-Sum of All K-Long Subarrays II -> [LeetCode](https://leetcode.com/problems/find-x-sum-of-all-k-long-subarrays-ii/description)

Hard
 
You are given an array nums of n integers and two integers k and x.

The x-sum of an array is calculated by the following procedure:

Count the occurrences of all elements in the array.
Keep only the occurrences of the top x most frequent elements. If two elements have the same number of occurrences, the element with the bigger value is considered more frequent.
Calculate the sum of the resulting array.
Note that if an array has less than x distinct elements, its x-sum is the sum of the array.

Return an integer array answer of length n - k + 1 where answer[i] is the x-sum of the subarray nums[i..i + k - 1].

 

Example 1:

Input: nums = [1,1,2,2,3,4,2,3], k = 6, x = 2

Output: [6,10,12]

Explanation:

For subarray [1, 1, 2, 2, 3, 4], only elements 1 and 2 will be kept in the resulting array. Hence, answer[0] = 1 + 1 + 2 + 2.
For subarray [1, 2, 2, 3, 4, 2], only elements 2 and 4 will be kept in the resulting array. Hence, answer[1] = 2 + 2 + 2 + 4. Note that 4 is kept in the array since it is bigger than 3 and 1 which occur the same number of times.
For subarray [2, 2, 3, 4, 2, 3], only elements 2 and 3 are kept in the resulting array. Hence, answer[2] = 2 + 2 + 2 + 3 + 3.
Example 2:

Input: nums = [3,8,7,8,7,5], k = 2, x = 2

Output: [11,15,15,15,12]

Explanation:

Since k == x, answer[i] is equal to the sum of the subarray nums[i..i + k - 1].

 

Constraints:

nums.length == n
1 <= n <= 105
1 <= nums[i] <= 109
1 <= x <= k <= nums.length


# Code
```cpp []
#define ll long long

class comp1{
public:
    //{least frequent, smaller number}
    bool operator()(auto &a,auto &b) const{
        if(a.first==b.first) return a.second<b.second;

        return a.first<b.first;
    }
};

class comp2{
public:
    // {most frequent,bigger number}
    bool operator()(auto &a,auto &b) const{
        if(a.first==b.first) return a.second>b.second;

        return a.first>b.first;
    }
};

class Solution {
public:
    vector<long long> findXSum(vector<int>& nums, int k, int x) {
        int n=nums.size();
        //map to keep frequency of each element
        unordered_map<int ,ll>mp;
        //sum to keep final sum after each window
        ll sum=0;
        for(int i=0;i<k;i++)
        {
            mp[nums[i]]++;
        }
        int i=0;
        vector<ll>ans;
        set<pair<ll,int>,comp1>s1;//up->most likely to get out from here
        set<pair<ll,int>,comp2>s2,s;//up->most likely to come in s1

        for(auto &val: mp)
        {
            s.insert({val.second,val.first});
        }
        int cnt=0;
        //tranfer element belonging to appropriate set s1 or s2
        while(!s.empty())
        {
            auto [c,v]=*s.begin();
            s.erase(s.begin());
            if(cnt<x)
            {
                s1.insert({c,v});
                sum+=c*v;
            }
            else
            {
                s2.insert({c,v});
            }
            cnt++;
        }
        ans.push_back(sum);
        //window from i to j
        //NOTE: whenever s1 is update sum will also be updated
        for(int j=k;j<n;j++)
        {
            //now remove all cases because of number nums[i]
            if(s1.find({mp[nums[i]],nums[i]})==s1.end())
            {
                //found in s2
                auto it=s2.find({mp[nums[i]],nums[i]});
                // it->first--;
                if(it!=s2.end())
                {
                    s2.erase(it);
                }
                s2.insert({mp[nums[i]]-1,nums[i]});
                mp[nums[i]]--;
            }
            else
            {
                //found in s1
                auto it=s1.find({mp[nums[i]],nums[i]});
                // *it->first--;
                if(it!=s1.end())s1.erase(it);
                s1.insert({mp[nums[i]]-1,nums[i]});
                mp[nums[i]]--;
                sum-=nums[i];
            }
            i++;
            //now remove all cases because of nums[j]
            if(s1.find({mp[nums[j]],nums[j]})==s1.end())
            {
                //found in s2
                auto it=s2.find({mp[nums[j]],nums[j]});
                // *it->first++;
                if(it!=s2.end())s2.erase(it);
                s2.insert({mp[nums[j]]+1,nums[j]});
                mp[nums[j]]++;
            }
            else
            {
                //found in s1
                auto it=s1.find({mp[nums[j]],nums[j]});
                // *it->first++;
                if(it!=s1.end())s1.erase(it);
                s1.insert({mp[nums[j]]+1,nums[j]});
                mp[nums[j]]++;
                sum+=nums[j];
            }
            //make size of set s1 to x if possible
            while(s1.size()<x && s2.size()>0)
            {
                auto v2=*s2.begin();
                s2.erase(s2.begin());
                s1.insert(v2);
                sum+=v2.first*v2.second;
            }
            //now swap the positions of top of s1 and top of s2 if:
            // 1-> top frequency count of s1 < top frequency count of s2
            // 2-> if frequency equal and s1 element value < s2 element value
            while(s2.size()>0)
            {
                auto v1=*s1.begin();
                auto v2=*s2.begin();
                if(v1.first<v2.first || (v1.first==v2.first && v1.second<v2.second))
                {
                    sum-=v1.first*v1.second;
                    sum+=v2.first*v2.second;
                    s1.erase(s1.begin());
                    s2.erase(s2.begin());
                    s1.insert({v2.first,v2.second});
                    s2.insert({v1.first,v1.second});
                }
                else break;
            }
            ans.push_back(sum);
        }
        return ans;
    }
};
```

--------------------------------------------------------------------------------------------

