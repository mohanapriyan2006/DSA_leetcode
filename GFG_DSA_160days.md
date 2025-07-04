-----------------------------------------------
# Geeks For Geeks - 160 Days ( DSA challenge )
-----------------------------------------------

## Second Largest -> [GFG](https://www.geeksforgeeks.org/batch/gfg-160-problems/track/arrays-gfg-160/problem/second-largest3735)

Difficulty: Easy

Given an array of positive integers arr[], return the second largest element from the array. If the second largest element doesn't exist then return -1.

Note: The second largest element should not be equal to the largest element.

Examples:

Input: arr[] = [12, 35, 1, 10, 34, 1]
Output: 34
Explanation: The largest element of the array is 35 and the second largest element is 34.

Input: arr[] = [10, 5, 10]
Output: 5
Explanation: The largest element of the array is 10 and the second largest element is 5.

Input: arr[] = [10, 10, 10]
Output: -1
Explanation: The largest element of the array is 10 and the second largest element does not exist.

Constraints:

2 ≤ arr.size() ≤ 105
1 ≤ arr[i] ≤ 105

Expected Complexities

Time Complexity: O(n)
Auxiliary Space: O(1)

Company Tags
SAP Labs Rockstand

Topic Tags
Arrays SearchingData Structures Algorithms

# Code
```cpp []
class Solution {
  public:
    int getSecondLargest(vector<int> &arr) {
        
        int N = arr.size();
        
        int fl = -1, sl = -1;
        
        for(int n:arr){
            if(n > fl){
                sl = fl;
                fl = n;
            }else if(n<fl && n>sl){
                sl = n;
            }
        }
        
        return sl;
    }
};
```

------


## Move All Zeroes to End -> [GFG](https://www.geeksforgeeks.org/batch/gfg-160-problems/track/arrays-gfg-160/problem/move-all-zeroes-to-end-of-array0751)
Difficulty: Easy

You are given an array arr[] of non-negative integers. Your task is to move all the zeros in the array to the right end while maintaining the relative order of the non-zero elements. The operation must be performed in place, meaning you should not use extra space for another array.

Examples:

Input: arr[] = [1, 2, 0, 4, 3, 0, 5, 0]
Output: [1, 2, 4, 3, 5, 0, 0, 0]
Explanation: There are three 0s that are moved to the end.

Input: arr[] = [10, 20, 30]
Output: [10, 20, 30]
Explanation: No change in array as there are no 0s.

Input: arr[] = [0, 0]
Output: [0, 0]
Explanation: No change in array as there are all 0s.

Constraints:

1 ≤ arr.size() ≤ 105
0 ≤ arr[i] ≤ 105

Expected Complexities

Time Complexity: O(n)
Auxiliary Space: O(1)

Company Tags

Paytm Amazon Microsoft Samsung SAP Labs Linkedin Bloomberg

Topic Tags

Arrays Data Structures

# Code
```cpp []
class Solution {
  public:
    void pushZerosToEnd(vector<int>& arr) {
        
        int n = arr.size();
        
        int j = 0;
        
        for(int  i=0 ; i< n ; ++i){
            if(arr[i] != 0) arr[j++] = arr[i];
        }
        
        while(j<n){
            arr[j++] = 0;
        }
    }
};
```

------

## Reverse an Array -> [GFG](https://www.geeksforgeeks.org/batch/gfg-160-problems/track/arrays-gfg-160/problem/reverse-an-array)
Difficulty: Easy

You are given an array of integers arr[]. Your task is to reverse the given array.

Note: Modify the array in place.

Examples:

Input: arr = [1, 4, 3, 2, 6, 5]
Output: [5, 6, 2, 3, 4, 1]
Explanation: The elements of the array are 1 4 3 2 6 5. After reversing the array, the first element goes to the last position, the second element goes to the second last position and so on. Hence, the answer is 5 6 2 3 4 1.

Input: arr = [4, 5, 2]
Output: [2, 5, 4]
Explanation: The elements of the array are 4 5 2. The reversed array will be 2 5 4.

Input: arr = [1]
Output: [1]
Explanation: The array has only single element, hence the reversed array is same as the original.

Constraints:

1<=arr.size()<=105
0<=arr[i]<=105

Expected Complexities

Time Complexity: O(n)
Auxiliary Space: O(1)

Company Tags

BloombergFacebookTCSAdobeGoogleInfosysCapgeminiMorgan StanleyAmazonMicrosoftAppleYahooPayPalUber

Topic Tags

Arrays Data Structures

# Code
```cpp []
class Solution {
  public:
    void reverseArray(vector<int> &arr) {
        int i = 0;
        int j = arr.size() - 1;
        
        while(i<j){
            int temp = arr[i];
            arr[i++] = arr[j];
            arr[j--] = temp;
        }
    }
};
```

------


## Rotate Array -> [GFG](https://www.geeksforgeeks.org/batch/gfg-160-problems/track/arrays-gfg-160/problem/rotate-array-by-n-elements-1587115621)
Difficulty: Medium

Given an array arr[]. Rotate the array to the left (counter-clockwise direction) by d steps, where d is a positive integer. Do the mentioned change in the array in place.

Note: Consider the array as circular.

Examples :

Input: arr[] = [1, 2, 3, 4, 5], d = 2
Output: [3, 4, 5, 1, 2]
Explanation: when rotated by 2 elements, it becomes 3 4 5 1 2.

Input: arr[] = [2, 4, 6, 8, 10, 12, 14, 16, 18, 20], d = 3
Output: [8, 10, 12, 14, 16, 18, 20, 2, 4, 6]
Explanation: when rotated by 3 elements, it becomes 8 10 12 14 16 18 20 2 4 6.

Input: arr[] = [7, 3, 9, 1], d = 9
Output: [3, 9, 1, 7]
Explanation: when we rotate 9 times, we'll get 3 9 1 7 as resultant array.

Constraints:

1 <= arr.size(), d <= 105
0 <= arr[i] <= 105

Expected Complexities

Time Complexity: O(n)
Auxiliary Space: O(1)

Company Tags

AmazonMicrosoftMAQ Software

Topic Tags

Arrays Data Structures

# Code
```cpp []
class Solution {
    private:
    void reverse(vector<int>& arr,int l,int h){
        while(l<=h) swap(arr[l++],arr[h--]);
    }
  public:
    
    void rotateArr(vector<int>& a, int k) {
        int len = a.size();
        k = k%len;
        if(k<0){
          k = k+len;
        }
        reverse(a,0,k-1);
        reverse(a,k,len-1);
        reverse(a,0,len-1);
    }
};
```

------



## Next Permutation -> [GFG](https://www.geeksforgeeks.org/batch/gfg-160-problems/track/arrays-gfg-160/problem/next-permutation5226)
Difficulty: Medium

Given an array of integers arr[] representing a permutation, implement the next permutation that rearranges the numbers into the lexicographically next greater permutation. If no such permutation exists, rearrange the numbers into the lowest possible order (i.e., sorted in ascending order). 

Note - A permutation of an array of integers refers to a specific arrangement of its elements in a sequence or linear order.

Examples:

Input: arr = [2, 4, 1, 7, 5, 0]
Output: [2, 4, 5, 0, 1, 7]
Explanation: The next permutation of the given array is {2, 4, 5, 0, 1, 7}.

Input: arr = [3, 2, 1]
Output: [1, 2, 3]
Explanation: As arr[] is the last permutation, the next permutation is the lowest one.

Input: arr = [3, 4, 2, 5, 1]
Output: [3, 4, 5, 1, 2]
Explanation: The next permutation of the given array is [3, 4, 5, 1, 2].

Constraints:

1 ≤ arr.size() ≤ 105
0 ≤ arr[i] ≤ 105


Company Tags

InfosysFlipkartAmazonMicrosoftFactSetHikeMakeMyTripGoogleQualcommSalesforce

Topic Tags

Arrayspermutationconstructive algoData Structures

# Code
```cpp []
class Solution {
  public:
    void nextPermutation(vector<int>& arr) {
        int n = arr.size();
        
        int pivot = -1;
        
        for(int i = n -2 ; i>=0 ; --i){
            if(arr[i] < arr[i+1]){
                pivot = i;
                break;
            }
        }
        
        if(pivot == -1){
            reverse(arr.begin(), arr.end());
            return;
        }
        
        for(int i=n-1 ; i>pivot ; --i){
            if(arr[pivot] < arr[i]){
                swap(arr[i],arr[pivot]);
                break;
            }
        }
        
        reverse(arr.begin() + pivot + 1,arr.end());
    }
};
```

------



## Majority Element II -> [GFG](https://www.geeksforgeeks.org/batch/gfg-160-problems/track/arrays-gfg-160/problem/majority-vote)
Difficulty: Medium

You are given an array of integer arr[] where each number represents a vote to a candidate. Return the candidates that have votes greater than one-third of the total votes, If there's not a majority vote, return an empty array. 

Note: The answer should be returned in an increasing format.

Examples:

Input: arr[] = [2, 1, 5, 5, 5, 5, 6, 6, 6, 6, 6]
Output: [5, 6]
Explanation: 5 and 6 occur more n/3 times.

Input: arr[] = [1, 2, 3, 4, 5]
Output: []
Explanation: o candidate occur more than n/3 times.

Constraint:

1 <= arr.size() <= 106
-109 <= arr[i] <= 109

Expected Complexities

Time Complexity: O(n)
Auxiliary Space: O(1)

# Code
```cpp []
class Solution {
  public:
    vector<int> findMajority(vector<int>& arr) {
        
        vector<int> ans;
        
        map<int,int> freq;
        
        for(int num:arr){
            freq[num]++;
        }
        
        int n = arr.size()/3;
        
        for(auto it:freq){
            if(it.second > n) ans.push_back(it.first);
        }
        
        return ans;
        
    }
};
```

------



## Stock Buy and Sell – Max one Transaction Allowed -> [GFG](https://www.geeksforgeeks.org/batch/gfg-160-problems/track/arrays-gfg-160/problem/buy-stock-2)

Difficulty: Easy

Given an array prices[] of length n, representing the prices of the stocks on different days. The task is to find the maximum profit possible by buying and selling the stocks on different days when at most one transaction is allowed. Here one transaction means 1 buy + 1 Sell. If it is not possible to make a profit then return 0.

Note: Stock must be bought before being sold.

Examples:

Input: prices[] = [7, 10, 1, 3, 6, 9, 2]
Output: 8
Explanation: You can buy the stock on day 2 at price = 1 and sell it on day 5 at price = 9. Hence, the profit is 8.

Input: prices[] = [7, 6, 4, 3, 1]
Output: 0 
Explanation: Here the prices are in decreasing order, hence if we buy any day then we cannot sell it at a greater price. Hence, the answer is 0.

Input: prices[] = [1, 3, 6, 9, 11]
Output: 10 
Explanation: Since the array is sorted in increasing order, we can make maximum profit by buying at price[0] and selling at price[n-1].

Constraint:

1 <= prices.size()<= 105
0 <= prices[i] <=104

Expected Complexities

Time Complexity: O(n)
Auxiliary Space: O(1)

Company Tags

Bloomberg Facebook Intel Infosys Zoho MorganStanley Amazon Microsoft Samsung YahooPayPalNvidiaOracleVisaWalmartGoldman SachsTCSAdobeGoogleIBMAccentureAppleUber

Topic Tags

Greedy Arrays

# Code
```cpp []
class Solution {
  public:
    int maximumProfit(vector<int> &arr) {
        int n = arr.size();
        
        int minPrice = arr[0];
        
        int profit = 0;
        
        for(int i=1 ; i<n ; ++i){
            if(arr[i] > minPrice){
                profit = max(profit, arr[i] - minPrice);
            }
            else{
                minPrice = arr[i];
            }
        }
        
        return profit;
    }
};

```

------



# Quick Sort -> [link](https://www.geeksforgeeks.org/problems/quick-sort/1) (GFG)

Difficulty: Medium
Implement Quick Sort, a Divide and Conquer algorithm, to sort an array, arr[] in ascending order. Given an array, arr[], with starting index low and ending index high, complete the functions partition() and quickSort(). Use the last element as the pivot so that all elements less than or equal to the pivot come before it, and elements greater than the pivot follow it.

Note: The low and high are inclusive.

Examples:

Input: arr[] = [4, 1, 3, 9, 7]

Output: [1, 3, 4, 7, 9]

Explanation: After sorting, all elements are arranged in ascending order.


Input: arr[] = [2, 1, 6, 10, 4, 1, 3, 9, 7]

Output: [1, 1, 2, 3, 4, 6, 7, 9, 10]

Explanation: Duplicate elements (1) are retained in sorted order.


Input: arr[] = [5, 5, 5, 5]

Output: [5, 5, 5, 5]

Explanation: All elements are identical, so the array remains unchanged.


Constraints:
1 <= arr.size() <= 105
1 <= arr[i] <= 105

Expected Complexities
Time Complexity: O(n log n)
Auxiliary Space: O(log n)

Company Tags
VMWare Amazon Microsoft Samsung Hike Ola  Cabs Goldman Sachs Adobe SAP Labs Qualcomm HSBC Grofers Target Corporation


```cpp []
class Solution {
  public:
    void quickSort(vector<int>& arr, int low, int high) {
        if(low<high){
            int part = partition(arr,low,high);
            quickSort(arr,low,part-1);
            quickSort(arr,part+1,high);
        }
        
    }

  public:
    int partition(vector<int>& arr, int low, int high) {
        int pivot = arr[low];
        int i = low;
        int j = high;
        
        while(i<j){
            while(pivot >= arr[i] && i<high){
                i++;
            }
            while(pivot < arr[j] && j>low){
                j--;
            }
            
            if(i<j) swap(arr[i],arr[j]);
        }
        
        swap(arr[low],arr[j]);
        
        return j;
    }
};
```

----



## Partition Equal Subset Sum -> [GFG](https://www.geeksforgeeks.org/problems/subset-sum-problem2014/1)
Difficulty: Medium

Given an array arr[], determine if it can be partitioned into two subsets such that the sum of elements in both parts is the same.

Note: Each element must be in exactly one subset.

Examples:

Input: arr = [1, 5, 11, 5]
Output: true
Explanation: The two parts are [1, 5, 5] and [11].

Input: arr = [1, 3, 5]
Output: false
Explanation: This array can never be partitioned into two such parts.

Constraints:

1 ≤ arr.size ≤ 100
1 ≤ arr[i] ≤ 200

Expected Complexities

Time Complexity: O(sum(arr) * n)
Auxiliary Space: O(sum(arr))

Company Tags

AccoliteAmazonMicrosoftOYO RoomsAdobeDrishti-Soft

Topic Tags

Dynamic ProgrammingsubsetAlgorithms

# Code
```cpp []
class Solution {
  public:
    bool equalPartition(vector<int>& arr) {
        int total = 0 ;
        
        for(const int num:arr){
            total+=num;
        }
        
        if(total % 2 != 0) return false;
        
        int target = total / 2;
        
        vector<bool> dp(target+1 , false);
        
        dp[0] = true;
        
        for(int i=0 ; i < arr.size() ; ++i){
            for(int j = target ; j>= arr[i] ; --j){
                dp[j] = dp[j] || dp[ j - arr[i] ];
            }
        }
        
        return dp[target];
        
    }
};
```

------


## Median of 2 Sorted Arrays of Different Sizes -> [GFG](https://www.geeksforgeeks.org/problems/median-of-2-sorted-arrays-of-different-sizes/1)
Difficulty: Hard

Given two sorted arrays a[] and b[], find and return the median of the combined array after merging them into a single sorted array.

Examples:

Input: a[] = [-5, 3, 6, 12, 15], b[] = [-12, -10, -6, -3, 4, 10]
Output: 3
Explanation: The merged array is [-12, -10, -6, -5, -3, 3, 4, 6, 10, 12, 15]. So the median of the merged array is 3.

Input: a[] = [2, 3, 5, 8], b[] = [10, 12, 14, 16, 18, 20]
Output: 11
Explanation: The merged array is [2, 3, 5, 8, 10, 12, 14, 16, 18, 20]. So the median of the merged array is (10 + 12) / 2 = 11.

Input: a[] = [], b[] = [2, 4, 5, 6]
Output: 4.5
Explanation: The merged array is [2, 4, 5, 6]. So the median of the merged array is (4 + 5) / 2 = 4.5.

Constraints: 

0 ≤ a.size(), b.size() ≤ 106
1 ≤ a[i], b[i] ≤ 109
a.size() + b.size() > 0

Expected Complexities

Time Complexity: O(log(min(n, m)))
Auxiliary Space: O(1)

Company Tags

AmazonMicrosoftSamsungGoogle

Topic Tags

ArraysData StructuresAlgorithmsBinary Search


# Code
```cpp []
class Solution {
  public:
    bool equalPartition(vector<int>& arr) {
        int total = 0 ;
        
        for(const int num:arr){
            total+=num;
        }
        
        if(total % 2 != 0) return false;
        
        int target = total / 2;
        
        vector<bool> dp(target+1 , false);
        
        dp[0] = true;
        
        for(int i=0 ; i < arr.size() ; ++i){
            for(int j = target ; j>= arr[i] ; --j){
                dp[j] = dp[j] || dp[ j - arr[i] ];
            }
        }
        
        return dp[target];
        
    }
};
```

------



## Two Sum - Pair with Given Sum -> [GFG](https://www.geeksforgeeks.org/problems/key-pair5616/1)
Difficulty: Easy

Given an array arr[] of positive integers and another integer target. Determine if there exist two distinct indices such that the sum of their elements is equal to the target.

Examples:

Input: arr[] = [1, 4, 45, 6, 10, 8], target = 16
Output: true
Explanation: arr[3] + arr[4] = 6 + 10 = 16.

Input: arr[] = [1, 2, 4, 3, 6], target = 11
Output: false
Explanation: None of the pair makes a sum of 11.

Input: arr[] = [11], target = 11
Output: false
Explanation: No pair is possible as only one element is present in arr[].

Constraints:

1 ≤ arr.size ≤ 105
1 ≤ arr[i] ≤ 105
1 ≤ target ≤ 2*105

Expected Complexities

Time Complexity: O(n)
Auxiliary Space: O(n)

Company Tags

ZohoFlipkartMorgan StanleyAccoliteAmazonMicrosoftFactSetHikeAdobeGoogleWiproSAP LabsCarWale

Topic Tags

ArraysHashData Structures

# Code
```cpp []
class Solution {
  public:
    bool twoSum(vector<int>& arr, int target) {
        
        int n = arr.size();
        
        unordered_map<int,int> seen;
        
        for(int i=0 ; i<n ; ++i){
            if( seen.find( target - arr[i] ) != seen.end() ) return true;
            seen[arr[i]] = i;
        }
        
        return false;
    }
};
```

------




## Minimize the Heights II -> [GFG](https://www.geeksforgeeks.org/batch/gfg-160-problems/track/arrays-gfg-160/problem/minimize-the-heights3351)
Difficulty: Medium

Given an array arr[] denoting heights of N towers and a positive integer K.

For each tower, you must perform exactly one of the following operations exactly once.

Increase the height of the tower by K
Decrease the height of the tower by K
Find out the minimum possible difference between the height of the shortest and tallest towers after you have modified each tower.

You can find a slight modification of the problem here.
Note: It is compulsory to increase or decrease the height by K for each tower. After the operation, the resultant array should not contain any negative integers.

Examples :

Input: k = 2, arr[] = {1, 5, 8, 10}
Output: 5
Explanation: The array can be modified as {1+k, 5-k, 8-k, 10-k} = {3, 3, 6, 8}.The difference between the largest and the smallest is 8-3 = 5.


Input: k = 3, arr[] = {3, 9, 12, 16, 20}
Output: 11
Explanation: The array can be modified as {3+k, 9+k, 12-k, 16-k, 20-k} -> {6, 12, 9, 13, 17}.The difference between the largest and the smallest is 17-6 = 11. 


Constraints

1 ≤ k ≤ 107
1 ≤ n ≤ 105
1 ≤ arr[i] ≤ 107

Expected Complexities

Time Complexity: O(n log n)
Auxiliary Space: O(1)


Company Tags

MicrosoftAdobe


Topic Tags

ArraysGreedyData StructuresAlgorithms

# Code
```cpp []


class Solution {
  public:
    int getMinDiff(vector<int> &arr, int k) {
        int n = arr.size();
        
        sort(arr.begin() , arr.end());
        
        int res = arr[n-1] - arr[0];
        
        for(int i=1 ; i<n ; ++i){
            if(arr[i] - k < 0) continue;
            int mini = min(arr[0] + k , arr[i] - k);
            int maxx = max(arr[i-1] + k , arr[n-1] - k);
            
            res = min(res,maxx - mini);
        }
        
        return res;
    }
};
```

------



## Anagram -> [GFG](https://www.geeksforgeeks.org/batch/gfg-160-problems/track/string-gfg-160/problem/anagram-1587115620)
Difficulty: Easy

Given two non-empty strings s1 and s2, consisting only of lowercase English letters, determine whether they are anagrams of each other or not. Two strings are considered anagrams if they contain the same characters with exactly the same frequencies, regardless of their order.

Examples:

Input: s1 = "geeks" s2 = "kseeg"
Output: true 
Explanation: Both the string have same characters with same frequency. So, they are anagrams. 

Input: s1 = "allergy", s2 = "allergyy" 
Output: false 
Explanation: Although the characters are mostly the same, s2 contains an extra 'y' character. Since the frequency of characters differs, the strings are not anagrams. 

Input: s1 = "listen", s2 = "lists" 
Output: false 
Explanation: The characters in the two strings are not the same — some are missing or extra. So, they are not anagrams.


Constraints:

1 ≤ s1.size(), s2.size() ≤ 105
s1, s2 consists of lowercase English letters.

Expected Complexities

Time Complexity: O(n + m)
Auxiliary Space: O(1)


Company Tags

FlipkartDirectiAdobeGoogleNagarroMedia.net


Topic Tags

StringsSortingData StructuresAlgorithms

# Code
```cpp []

class Solution {
  public:
    bool areAnagrams(string& s1, string& s2) {
        if(s1.size() != s2.size()) return false;
        
        vector<int> freq(26,0);
        
        for(const char c:s1) freq[c - 'a']++;
        for(const char c:s2) freq[c - 'a']--;
        
        for(const int n:freq){
            if(n != 0) return false;
        }
        
        return true;
    }
};
```

------



## Non Repeating Character -> [GFG](https://www.geeksforgeeks.org/batch/gfg-160-problems/track/string-gfg-160/problem/non-repeating-character-1587115620)
Difficulty: Easy

Given a string s consisting of lowercase English Letters. Return the first non-repeating character in s.
If there is no non-repeating character, return '$'.
Note: When you return '$' driver code will output -1.

Examples:

Input: s = "geeksforgeeks"
Output: 'f'
Explanation: In the given string, 'f' is the first character in the string which does not repeat.

Input: s = "racecar"
Output: 'e'
Explanation: In the given string, 'e' is the only character in the string which does not repeat.

Input: s = "aabbccc"
Output: -1
Explanation: All the characters in the given string are repeating.


Constraints:

1 ≤ s.size() ≤ 105


Expected Complexities

Time Complexity: O(n)
Auxiliary Space: O(1)


Company Tags

FlipkartAmazonMicrosoftD-E-ShawMakeMyTripOla CabsPayuTeradataGoldman SachsMAQ SoftwareInfoEdgeOATS SystemsTejas Network


Topic Tags

HashStringsData Structures

# Code
```cpp []

class Solution {
  public:
    char nonRepeatingChar(string &s) {
        
        vector<int> freq(26,0);
        
        for(const char c:s) freq[c - 'a']++;
        
        for(const char c:s){
            if(freq[c - 'a'] == 1) return c;
        }
        
        return '$';
    }
};
```

------


