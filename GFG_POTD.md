
----------------------------------------------------
# Geeks For Geeks - ***problem of the day*** (POTD)
----------------------------------------------------

# Maximize median after doing k addition operation -> [GFG](https://www.geeksforgeeks.org/problems/maximize-median-after-doing-k-addition-operation/1)

Difficulty: Medium

Given an array arr[] consisting of positive integers and an integer k. You are allowed to perform at most k operations, where in each operation, you can increment any one element of the array by 1.

Determine the maximum possible median of the array that can be achieved after performing at most k such operations.

Examples:

Input: arr[] = [1, 3, 4, 5], k = 3
Output: 5
Explanation: We can add +2 to the second element and +1 to the third element to get the array [1, 5, 5, 5]. After sorting, the array remains [1, 5, 5, 5]. Since the length is even, the median is (5 + 5) / 2 = 5.


Input: arr[] = [1, 3, 6, 4, 2], k = 10
Output: 7
Explanation: After applying operations optimally, we can transform the array to [1, 3, 7, 7, 7] (one possible way). Sorted array becomes [1, 3, 7, 7, 7]. Since the length is odd, the median is the middle element 7.


Constraints:

1 ≤ arr.size() ≤ 105
0 ≤ arr[i], k ≤ 109


Expected Complexities

Time Complexity: O(n * log k)
Auxiliary Space: O(1)


Topic Tags

Binary SearchAlgorithms


# code 
```cpp []
class Solution {
    bool isPossible(vector<int>& arr, int target, int k){
        int n = arr.size();
    
        if (n % 2 == 1) {
            // for odd-sized array, consider elements from 
            // middle to end
            for (int i = n / 2; i < n; ++i) {
                if (arr[i] < target)
                    k -= (target - arr[i]);
            }
        } 
        else {
        
            if (arr[n / 2] <= target) {
                k -= (target - arr[n / 2]);
                k -= (target - arr[n / 2 - 1]);
            } 
            else {
                k -= (2 * target - 
                        (arr[n / 2] + arr[n / 2 - 1]));
            }
            
            for (int i = n / 2 + 1; i < n; ++i) {
                if (arr[i] < target)
                    k -= (target - arr[i]);
            }
        }
    
        return k >= 0;
    }


  public:
    int maximizeMedian(vector<int>& arr, int k) {
        int n = arr.size();
        sort(arr.begin(), arr.end());
    
        int iniMedian = arr[n / 2];
        if (n % 2 == 0) {
            iniMedian += arr[n / 2 - 1];
            iniMedian /= 2;
        }
    
        int low = iniMedian, high = iniMedian + k;
        int bestMedian = iniMedian;
    
        while (low <= high) {
            int mid = (low + high) / 2;
    
            if (isPossible(arr, mid, k)) {
                bestMedian = mid;
                low = mid + 1;
            } 
            else {
                high = mid - 1;
            }
        }
    
        return bestMedian;
    }
};
```


--------------------------------


# Check if a String is Subsequence of Other -> [GFG](https://www.geeksforgeeks.org/problems/given-two-strings-find-if-first-string-is-a-subsequence-of-second/1)

Difficulty: Easy

Given two strings s1 and s2. You have to check that s1 is a subsequence of s2 or not.
Note: A subsequence is a sequence that can be derived from another sequence by deleting some elements without changing the order of the remaining elements.

Examples:

Input: s1 = "AXY", s2 = "YADXCP"
Output: false
Explanation: s1 is not a subsequence of s2 as 'Y' appears before 'A'.

Input: s1 = "gksrek", s2 = "geeksforgeeks"
Output: true
Explanation: If we combine the bold character of "geeksforgeeks", it equals to s1. So s1 is a subsequence of s2. 


Constraints:

1 ≤ s1.size(), s2.size() ≤ 106


Expected Complexities

Time Complexity: O(n)
Auxiliary Space: O(1)


Topic Tags

StringsGreedytwo-pointer-algorithm


# code 
```cpp []
class Solution {
  public:
    bool isSubSeq(string& s1, string& s2) {
        int n = s1.size(), m = s2.size();
        if(n>m) return false;
        int i=0 , j=0;
        while(i<n && j<m){
            if(s1[i] == s2[j]) i++;
            j++;
        }
        return i==n;
    }
};
```


--------------------------------


# Count the number of possible triangles -> [GFG](https://www.geeksforgeeks.org/problems/count-possible-triangles-1587115620/1)

Difficulty: Medium

Given an integer array arr[]. Find the number of triangles that can be formed with three different array elements as lengths of three sides of the triangle. A triangle with three given sides is only possible if sum of any two sides is always greater than the third side.

Examples:

Input: arr[] = [4, 6, 3, 7]
Output: 3
Explanation: There are three triangles possible [3, 4, 6], [4, 6, 7] and [3, 6, 7]. Note that [3, 4, 7] is not a possible triangle.  

Input: arr[] = [10, 21, 22, 100, 101, 200, 300]
Output: 6
Explanation: There can be 6 possible triangles: [10, 21, 22], [21, 100, 101], [22, 100, 101], [10, 100, 101], [100, 101, 200] and [101, 200, 300].

Input: arr[] = [1, 2, 3]
Output: 0
Explanation: No triangles are possible.


Constraints:

1 ≤ arr.size() ≤ 103
0 ≤ arr[i] ≤ 105


Expected Complexities

Time Complexity: O(n^2)
Auxiliary Space: O(1)


Company Tags

AmazonMicrosoft


Topic Tags

ArraysSortingData StructuresAlgorithms


# code 
```cpp []
class Solution {
  public:
    int countTriangles(vector<int>& arr) {
        int res = 0;
    sort(arr.begin(), arr.end());

    // Iterate through the array, fixing 
    // the largest side at arr[i]
    for (int i = 2; i < arr.size(); ++i) {
      
      	// Initialize pointers for the two smaller sides
        int left = 0, right = i - 1; 

        while (left < right) {
          
            if (arr[left] + arr[right] > arr[i]) {
              
                // arr[left] + arr[right] satisfies 
                // the triangle inequality, so all pairs
				// (x, right) with (left <= x < right) are valid
                res += right - left; 
              
              	// Move the right pointer to check smaller pairs
                right--; 
            } 
          	else {
              
              	// Move the left pointer to increase the sum
                left++; 
            }
        }
    }

    return res;
    }
};

```


--------------------------------


# Smallest window containing all characters -> [GFG](https://www.geeksforgeeks.org/problems/smallest-window-in-a-string-containing-all-the-characters-of-another-string-1587115621/1)

Difficulty: Hard

Given two strings s and p. Find the smallest substring in s consisting of all the characters (including duplicates) of the string p. Return empty string in case no such substring is present.
If there are multiple such substring of the same length found, return the one with the least starting index.

Examples:

Input: s = "timetopractice", p = "toc"
Output: "toprac"
Explanation: "toprac" is the smallest substring in which "toc" can be found.


Input: s = "zoomlazapzo", p = "oza"
Output: "apzo"
Explanation: "apzo" is the smallest substring in which "oza" can be found.

Input: s = "zoom", p = "zooe"
Output: ""
Explanation: No substring is present containing all characters of p.


Constraints: 

1 ≤ s.length(), p.length() ≤ 106
s, p consists of lowercase english letters


Expected Complexities

Time Complexity: O(n)
Auxiliary Space: O(1)


Company Tags

FlipkartAmazonMicrosoftMakeMyTripGoogleStreamoid TechnologiesMedia.netAtlassian


Topic Tags

sliding-windowHashStringsDynamic ProgrammingBinary Search


# code 
```cpp []
class Solution {
  public:
    string smallestWindow(string &s, string &p) {
        int len1 = s.length();
        int len2 = p.length();
    
        if (len1 < len2)
            return "";
    
        vector<int> countP(256, 0);
        vector<int> countS(256, 0);
    
        
        for (int i = 0; i < len2; i++)
            countP[p[i]]++;
    
        int start = 0, start_idx = -1, min_len = INT_MAX;
    
        int count = 0;
    
        for (int j = 0; j < len1; j++){
            
            countS[s[j]]++;
    
            if (countP[s[j]] != 0 && countS[s[j]] <= countP[s[j]]){
                count++;
            }
    
            if (count == len2){
                while (countS[s[start]] > countP[s[start]] || 
                       countP[s[start]] == 0){
                    if (countS[s[start]] > countP[s[start]]){
                        countS[s[start]]--;
                    }
                    start++;
                }
    
                int len = j - start + 1;
                if (min_len > len){
                    min_len = len;
                    start_idx = start;
                }
            }
        }
    
        if (start_idx == -1)
            return "";
    
        return s.substr(start_idx, min_len);
    }
};

```


--------------------------------

# The Celebrity Problem -> [GFG](https://www.geeksforgeeks.org/problems/the-celebrity-problem/1)

Difficulty: Medium

A celebrity is a person who is known to all but does not know anyone at a party. A party is being organized by some people. A square matrix mat[][] of size n*n is used to represent people at the party such that if an element of row i and column j is set to 1 it means ith person knows jth person. You need to return the index of the celebrity in the party, if the celebrity does not exist, return -1.

Note: Follow 0-based indexing.

Examples:

Input: mat[][] = [[1, 1, 0],
                [0, 1, 0],
                [0, 1, 1]]
Output: 1

Explanation: 0th and 2nd person both know 1st person and 1st person does not know anyone. Therefore, 1 is the celebrity person.


Input: mat[][] = [[1, 1], 
                [1, 1]]
Output: -1

Explanation: Since both the people at the party know each other. Hence none of them is a celebrity person.


Input: mat[][] = [[1]]
Output: 0


Constraints:

1 ≤ mat.size() ≤ 1000
0 ≤ mat[i][j] ≤ 1
mat[i][i] = 1


Expected Complexities

Time Complexity: O(n)
Auxiliary Space: O(1)


Company Tags

ZohoFlipkartAmazonMicrosoftGoogleFab.comOne97United Health Group


Topic Tags

ArraysStackData Structurestwo-pointer-algorithm


```cpp []
class Solution {
  public:
    int celebrity(vector<vector<int>>& mat) {
        int n = mat.size();

        int i = 0, j = n - 1;
        while (i < j) {
            
            if (mat[j][i] == 1) 
                j--;
    
            else
                i++;
        }
    
        int c = i;
    
      
        for (i = 0; i < n; i++) {
            if(i == c) continue;
    
            if (mat[c][i] || !mat[i][c])
                return -1;
        }
    
        return c;
    }
};
```

--------------------------------


# Container With Most Water -> [GFG](https://www.geeksforgeeks.org/problems/container-with-most-water0535/1)

Difficulty: Medium

Given an array arr[] of non-negative integers, where each element arr[i] represents the height of the vertical lines, find the maximum amount of water that can be contained between any two lines, together with the x-axis.

Note: In the case of a single vertical line it will not be able to hold water.

Examples:

Input: arr[] = [1, 5, 4, 3]
Output: 6
Explanation: 5 and 3 are 2 distance apart. So the size of the base is 2. Height of container = min(5, 3) = 3. So, total area to hold water = 3 * 2 = 6.


Input: arr[] = [3, 1, 2, 4, 5]
Output: 12
Explanation: 5 and 3 are 4 distance apart. So the size of the base is 4. Height of container = min(5, 3) = 3. So, total area to hold water = 4 * 3 = 12.


Input: arr[] = [2, 1, 8, 6, 4, 6, 5, 5]
Output: 25 
Explanation: 8 and 5 are 5 distance apart. So the size of the base is 5. Height of container = min(8, 5) = 5. So, the total area to hold water = 5 * 5 = 25.


Constraints:

1 ≤ arr.size() ≤ 105
0 ≤ arr[i] ≤ 104


Expected Complexities

Time Complexity: O(n)
Auxiliary Space: O(1)


Company Tags

FlipkartAmazonGoogle


Topic Tags

ArraysMathematicaltwo-pointer-algorithm

### code
```cpp []
class Solution {
  public:
    int maxWater(vector<int> &arr) {
        int left = 0, right = arr.size() - 1;
        int res = 0;
        while(left < right) {
            
            int water = min(arr[left], arr[right]) * (right - left);
            res = max(res, water);
          
            if(arr[left] < arr[right])
                left += 1;
            else
                right -= 1;
        }
  
        return res;
    }
};
```

-------------------

# Sum of Mode -> [GFG](https://www.geeksforgeeks.org/problems/sum-of-mode/1)

Difficulty: Hard

Given an array arr[] of positive integers and an integer k. You have to find the sum of the modes of all the subarrays of size k.
Note: The mode of a subarray is the element that occurs with the highest frequency. If multiple elements have the same highest frequency, the smallest such element is considered the mode.

Examples:

Input: arr[] = [1, 2, 3, 2, 5, 2, 4, 4], k = 3

Output: 13

Explanation: The mode of each k size subarray is [1, 2, 2, 2, 2, 4] and sum of all modes is 13.


Input: arr[] = [1, 2, 1, 3, 5], k = 2

Output: 6

Explanation: The mode of each k size subarray is [1, 1, 1, 3] and sum of all modes is 6.


Constraints:

1 ≤ k ≤ arr.size() ≤105
1 ≤ arr[i] ≤ 105


Expected Complexities

Time Complexity: O(n log k)
Auxiliary Space: O(k)


Topic Tags

Greedysetsliding-windowtwo-pointer-algorithmHash

## code

```cpp []
class Solution {
  public:
    int sumOfModes(vector<int>& arr, int k) {
        int n = arr.size();
        unordered_map<int, int> freq;          
        map<int, set<int>> freqToVals;  
        long long result = 0;
    
        auto add = [&](int x) {
            int oldFreq = freq[x];
            if (oldFreq > 0) {
                freqToVals[oldFreq].erase(x);
                if (freqToVals[oldFreq].empty())
                    freqToVals.erase(oldFreq);
            }
            freq[x]++;
            freqToVals[freq[x]].insert(x);
        };
    
        auto remove = [&](int x) {
            int oldFreq = freq[x];
            freqToVals[oldFreq].erase(x);
            if (freqToVals[oldFreq].empty())
                freqToVals.erase(oldFreq);
    
            freq[x]--;
            if (freq[x] > 0)
                freqToVals[freq[x]].insert(x);
        };
    
        
        for (int i = 0; i < k; i++) add(arr[i]);
        result += *freqToVals.rbegin()->second.begin();
    
        
        for (int i = k; i < n; i++) {
            add(arr[i]);
            remove(arr[i - k]);
            result += *freqToVals.rbegin()->second.begin();
        }
    
        return result;
    }
};
```

------------------------

# Swap Kth nodes from ends -> [GFG](https://www.geeksforgeeks.org/problems/swap-kth-node-from-beginning-and-kth-node-from-end-in-a-singly-linked-list/1)

Difficulty: Medium

Given the head of a singly linked list and an integer k. Swap the kth node (1-based index) from the beginning and the kth node from the end of the linked list. Return the head of the final formed list and if it's not possible to swap the nodes return the original list.

Examples:

Input: k = 1,

![img](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/701070/Web/Other/blobid0_1755953423.webp)
  
Output: 5 -> 2 -> 3 -> 4 -> 1

![img](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/701070/Web/Other/blobid1_1755953433.webp)

Explanation: Here k = 1, hence after swapping the 1st node from the beginning and end the new list will be 5 -> 2 -> 3 -> 4 -> 1.

![img](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/701070/Web/Other/blobid2_1755953453.webp)

Input: k = 2,
  
Output: 5 -> 9 -> 8 -> 5 -> 10 -> 3

![img](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/701070/Web/Other/blobid3_1755953462.webp)

Explanation: Here k = 2, hence after swapping the 2nd node from the beginning and end the new list will be 5 -> 9 -> 8 -> 5 -> 10 -> 3.
  

Constraints:

1 ≤ list size ≤ 104
1 ≤ node->data ≤ 106
1 ≤ k ≤ 104


Expected Complexities

Time Complexity: O(n)
Auxiliary Space: O(1)


Company Tags

Morgan StanleyAmazon


Topic Tags

Linked ListData Structures


### code
```cpp []
/*
class Node {
  public:
    int data;
    Node *next;

    Node(int x) {
        data = x;
        next = NULL;
    }
};
*/

class Solution {
  public:
    Node* swapKth(Node* head, int k) {
        if (!head) return nullptr;

        int n = 0;
        Node* temp = head;
        while (temp) {
            n++;
            temp = temp->next;
        }

        if (k > n) return head;


        if (2 * k - 1 == n) return head;

        Node *x_prev = nullptr, *x = head;
        for (int i = 1; i < k; i++) {
            x_prev = x;
            x = x->next;
        }


        Node *y_prev = nullptr, *y = head;
        for (int i = 1; i < n - k + 1; i++) {
            y_prev = y;
            y = y->next;
        }


        if (x_prev) x_prev->next = y;
        if (y_prev) y_prev->next = x;


        Node* tempNext = x->next;
        x->next = y->next;
        y->next = tempNext;


        if (k == 1) head = y;
        if (k == n) head = x;

        return head;
        
    }
};
```

----------------------------

# Reverse a Doubly Linked List -> [GFG](https://www.geeksforgeeks.org/problems/reverse-a-doubly-linked-list/1)

Difficulty: Easy

You are given the head of a doubly linked list. You have to reverse the doubly linked list and return its head.

Examples:

Input:

![img](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/908050/Web/Other/blobid0_1756123600.webp)
   
Output: 5 <-> 4 <-> 3
Explanation: After reversing the given doubly linked list the new list will be 5 <-> 4 <-> 3.
   
Input: 

![img](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/908050/Web/Other/blobid1_1756123728.webp)
   
Output: 196 <-> 59 <-> 122 <-> 75
Explanation: After reversing the given doubly linked list the new list will be 196 <-> 59 <-> 122 <-> 75.
   

Constraints:

1 ≤ number of nodes ≤ 106
0 ≤ node->data ≤ 104


Expected Complexities

Time Complexity: O(n)
Auxiliary Space: O(1)


Company Tags

D-E-ShawAdobe


Topic Tags

doubly-linked-listData Structures

## code
```cpp []

/*
class Node {
  public:
    int data;
    Node *next;
    Node *prev;
    Node(int val) {
        data = val;
        next = NULL;
        prev = NULL;
    }
};

*/
class Solution {
  public:
    Node *reverse(Node *head) {
        if(!head || !head->next) return head;
        
        Node* cur = head;
        Node* newHead = nullptr;
        
        while(cur){
            Node* temp = cur->prev;
            cur->prev = cur->next;
            cur->next = temp;
            newHead = cur;
            cur = cur->prev;
        }
        
        return newHead;
    
       
    }
};
```

------------------------



