




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


