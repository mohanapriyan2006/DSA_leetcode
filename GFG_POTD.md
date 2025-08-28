
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







