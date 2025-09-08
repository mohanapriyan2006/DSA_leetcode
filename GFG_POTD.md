
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

![img](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/908050/Web/Other/blobid1_1756123728.webp)

Explanation: After reversing the given doubly linked list the new list will be 5 <-> 4 <-> 3.
   
Input: 

![img](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/908050/Web/Other/blobid2_1756123773.webp)
   
Output: 196 <-> 59 <-> 122 <-> 75

![img](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/908050/Web/Other/blobid3_1756123876.webp)

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


# Linked List Group Reverse -> [GFG](https://www.geeksforgeeks.org/problems/reverse-a-linked-list-in-groups-of-given-size/1)

Difficulty: Hard

You are given the head of a Singly linked list. You have to reverse every k node in the linked list and return the head of the modified list.
Note: If the number of nodes is not a multiple of k then the left-out nodes at the end, should be considered as a group and must be reversed.

Examples:

Input: k = 2,

![img](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/908192/Web/Other/blobid0_1756125226.webp)
   
Output: 2 -> 1 -> 4 -> 3 -> 6 -> 5

![img](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/908192/Web/Other/blobid1_1756125284.webp)

Explanation: Linked List is reversed in a group of size k = 2.
   

Input: k = 4,

![img](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/908192/Web/Other/blobid2_1756125400.webp)
   
Output: 4 -> 3 -> 2 -> 1 -> 6 -> 5

![img](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/908192/Web/Other/blobid3_1756125453.webp)

Explanation: Linked List is reversed in a group of size k = 4.
   


Constraints:

1 ≤ size of linked list ≤ 105
0 ≤ node->data ≤ 106
1 ≤ k ≤ size of linked list 


Expected Complexities

Time Complexity: O(n)
Auxiliary Space: O(1)


Company Tags

PaytmVMWareAccoliteAmazonMicrosoftSnapdealHikeMakeMyTripWalmartGoldman SachsAdobeSAP Labs


Topic Tags

Linked ListData Structurestwo-pointer-algorithm

### code

```cpp []
/*
class Node {
  public:
    int data;
    Node* next;

    Node(int x){
        data = x;
        next = NULL;
    }
};
*/
class Solution {
  private:
    Node* findKNode(Node* temp , int k){
        k--;
        while(temp->next && k>0){
            k--;
            temp = temp->next;
        }
        return temp;
    }
    
    Node* revLL(Node* head){
        Node* pre = nullptr , *temp = head;
        while(temp){
            Node* nxt = temp->next;
            temp->next = pre;
            pre = temp;
            temp = nxt;
        }
        return pre;
    }
    
  public:
    Node *reverseKGroup(Node *head, int k) {
        if(!head || !head->next) return head;
        
        Node* cur = head , *preNode = nullptr;
        while(cur){
            Node* kNode = findKNode(cur , k);
            if(kNode == nullptr){
                if(preNode) preNode->next = cur;
                break;
            }
            Node* nxtNode = kNode->next;
            kNode->next = nullptr;
            
            revLL(cur);
            
            if(cur == head) head = kNode;
            else preNode->next = kNode;
            
            preNode = cur;
            cur = nxtNode;
        }
        
        return head;
        
    }
};
```

---------------

# Sort a linked list of 0s, 1s and 2s -> [GFG](https://www.geeksforgeeks.org/problems/given-a-linked-list-of-0s-1s-and-2s-sort-it/1)

Difficulty: Medium

Given the head of a linked list where nodes can contain values 0s, 1s, and 2s only. Your task is to rearrange the list so that all 0s appear at the beginning, followed by all 1s, and all 2s are placed at the end.

Examples:

Input: head = 1 → 2 → 2 → 1 → 2 → 0 → 2 → 2

![img](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/908245/Web/Other/blobid0_1756113569.jpg)
   
Output: 0 → 1 → 1 → 2 → 2 → 2 → 2 → 2

![img](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/908245/Web/Other/blobid1_1756113598.jpg)

Explanation: All the 0s are segregated to the left end of the linked list, 2s to the right end of the list, and 1s in between. The final list will be:
   


Input: head = 2 → 2 → 0 → 1

![img](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/908245/Web/Other/blobid2_1756113607.jpg)
   
Output: 0 → 1 → 2 → 2

![img](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/908245/Web/Other/blobid3_1756113615.jpg)

Explanation: After arranging all the 0s, 1s and 2s in the given format, the output will be:
   

Constraints:

1 ≤ no. of nodes ≤ 106
0 ≤ node->data ≤ 2


Expected Complexities

Time Complexity: O(n)
Auxiliary Space: O(1)


Company Tags

AmazonMicrosoftMakeMyTrip


Topic Tags

Linked ListData Structures


### code

```cpp []
/* Node is defined as
  class Node {
  public:
    int data;
    Node* next;

    Node(int x) {
        data = x;
        next = nullptr;
    }
};
*/
class Solution {
  public:
    Node* segregate(Node* head) {
        
        if(!head || !head->next) return head;
        
        Node* dummy0 = new Node(-1);
        Node* dummy1 = new Node(-1);
        Node* dummy2 = new Node(-1);
        
        Node* temp0 = dummy0;
        Node* temp1 = dummy1;
        Node* temp2 = dummy2;
        
        Node* cur = head;
        
        while(cur){
            if(cur->data == 0){
                temp0->next = cur;
                temp0 = cur;
            }
            else if(cur->data == 1){
                temp1->next = cur;
                temp1 = cur;
            }else{
                temp2->next = cur;
                temp2 = cur;
            }
            cur = cur->next;
        }
        
        temp0->next = dummy1->next ? dummy1->next : dummy2->next;
        temp1->next = dummy2->next;
        temp2->next = nullptr;
        
        return dummy0->next;
        
    }
};
```

-------------------------------


# Find length of Loop -> [GFG](https://www.geeksforgeeks.org/problems/find-length-of-loop/1)

Difficulty: Medium

Given the head of a linked list, determine whether the list contains a loop. If a loop is present, return the number of nodes in the loop, otherwise return 0.

Note: Internally, pos(1 based index) is used to denote the position of the node that tail's next pointer is connected to. If pos = 0, it means the last node points to null, indicating there is no loop. Note that pos is not passed as a parameter.

Examples:

Input: pos = 2,

![img1](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/904501/Web/Other/blobid0_1756186026.webp)
   
Output: 4

Explanation: There exists a loop in the linked list and the length of the loop is 4.


Input: pos = 3,

![img2](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/904501/Web/Other/blobid0_1756128118.webp)
   
Output: 3

Explanation: The loop is from 19 to 10. So length of loop is 19 → 33 → 10 = 3.


Input: pos = 0,

![img3](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/904501/Web/Other/blobid1_1756128178.webp)
    
Output: 0

Explanation: There is no loop.


Constraints:

1 ≤ number of nodes ≤ 105
1 ≤ node->data ≤ 104
0 ≤ pos < number of nodes


Expected Complexities

Time Complexity: O(n)
Auxiliary Space: O(1)


Company Tags

AmazonAdobeQualcomm


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
    int lengthOfLoop(Node *head) {
        Node *slow = head , *fast = head;
        while(fast && fast->next){
            slow = slow->next;
            fast = fast->next->next;
            if(slow == fast){
                int cnt = 1;
                fast = fast->next;
                while(fast != slow) cnt++, fast = fast->next;
                
                return cnt;
            }
        }
        return 0;
    }
};
```

--------------------------------------------------------------------

# Merge K sorted linked lists -> [GFG](https://www.geeksforgeeks.org/problems/merge-k-sorted-linked-lists/1)

Difficulty: Medium

Given an array arr[] of n sorted linked lists of different sizes. Your task is to merge all these lists into a single sorted linked list and return the head of the merged list.

Examples:

Input:

![img](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/908368/Web/Other/blobid0_1756363954.webp)
   
Output: 1 -> 2 -> 3 -> 4 -> 7 -> 8 -> 9

Explanation: The arr[] has 3 sorted linked list of size 3, 3, 1.
1st list: 1 -> 3 -> 7
2nd list: 2 -> 4 -> 8
3rd list: 9
The merged list will be: 

![img](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700265/Web/Other/blobid2_1756115425.jpg)
    

Input:

![img](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700265/Web/Other/blobid3_1756115435.jpg)

Output: 1 -> 3 -> 4 -> 5 -> 6 -> 8

Explanation: The arr[] has 3 sorted linked list of size 2, 1, 3.

1st list: 1 -> 3
2nd list: 8
3rd list: 4 -> 5 -> 6
The merged list will be: 

![img](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700265/Web/Other/blobid4_1756115445.jpg)

Constraints

1 ≤ total no. of nodes ≤ 105
1 ≤ node->data ≤ 103


Expected Complexities

Time Complexity: O(n log n)
Auxiliary Space: O(n)


Company Tags

VMWareAmazonMicrosoftOracle


Topic Tags

Linked ListHeapData StructuresMerge Sorttwo-pointer-algorithm


### code

```cpp []
/*
class Node {
  public:
    int data;
    Node* next;

    Node(int x){
        data = x;
        next = NULL;
    }
};
*/

class Solution {
  public:
    Node* mergeTwo(Node* head1, Node* head2) {
 
        Node* dummy = new Node(-1);
        Node* curr = dummy;
    
        while (head1 != nullptr && head2 != nullptr) {
          
            if (head1->data <= head2->data) {
                curr->next = head1;
                head1 = head1->next;
            } else {
                curr->next = head2;
                head2 = head2->next;
            }
            curr = curr->next;
        }
    
        if (head1 != nullptr) {
            curr->next = head1;
        } else {
            curr->next = head2;
        }
        return dummy->next;
    }
    
    Node* mergeListsRecur(int i, int j, vector<Node*> &arr) {
        
        if (i == j) return arr[i];
        
        int mid = i + (j-i)/2;
        Node* head1 = mergeListsRecur(i, mid, arr);
        
        Node* head2 = mergeListsRecur(mid+1, j, arr);
        
        Node* head = mergeTwo(head1, head2);
        
        return head;
    }
    
    Node* mergeKLists(vector<Node*>& arr) {
        
        if (arr.size()==0) return nullptr;
      
        return mergeListsRecur(0, arr.size()-1, arr);
    }
};
```

------------------------


# Merge Sort for Linked List
Difficulty: Medium

You are given the head of a linked list. You have to sort the given linked list using Merge Sort.

Examples:

Input:
    
Output: 10 -> 20 -> 30 -> 40 -> 50 -> 60

Explanation: After sorting the given linked list, the resultant list will be:
    

Input:
    
Output: 2 -> 5 -> 8 -> 9

Explanation: After sorting the given linked list, the resultant list will be:
    

Constraints:

1 ≤ number of nodes ≤ 105
0 ≤ node->data ≤ 106


Expected Complexities

Time Complexity: O(n log n)
Auxiliary Space: O(n)


Company Tags

PaytmAccoliteAmazonMicrosoftMAQ SoftwareAdobeVeritas


Topic Tags

Linked ListSortingMerge SortData StructuresAlgorithms


### code

```cpp []
/*
class Node {
public:
    int data;
    Node* next;

    Node(int x){
        data = x;
        next = NULL;
    }
};
*/
class Solution {
  private:
    Node* merge(Node* lf , Node* rt){
        Node* dummy = new Node(-1);
        Node *cur = dummy;
        while(lf && rt){
            if(lf->data < rt->data){
                cur->next = lf;
                lf = lf->next;
            }else{
                cur->next = rt;
                rt = rt->next;
            }
            cur = cur->next;
        }
        
        if(lf) cur->next = lf;
        else cur->next = rt;
        
        return dummy->next;
    }
  public:
    Node* mergeSort(Node* head) {
        if(!head || !head->next) return head;
        Node* slow = head , *fast = head->next;
        while(fast && fast->next){
            slow = slow->next;
            fast = fast->next->next;
        }
        Node *lf = head , *rt = slow->next;
        slow->next = nullptr;
        lf = mergeSort(lf);
        rt = mergeSort(rt);
        return merge(lf,rt);
    }
};
```

--------------------






