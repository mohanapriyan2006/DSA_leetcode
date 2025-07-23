
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



## Number of occurrence -> [GFG](https://www.geeksforgeeks.org/batch/gfg-160-problems/track/searching-gfg-160/problem/number-of-occurrence2259)
Difficulty: Easy

Given a sorted array, arr[] and a number target, you need to find the number of occurrences of target in arr[]. 

Examples :

Input: arr[] = [1, 1, 2, 2, 2, 2, 3], target = 2
Output: 4
Explanation: target = 2 occurs 4 times in the given array so the output is 4.

Input: arr[] = [1, 1, 2, 2, 2, 2, 3], target = 4
Output: 0
Explanation: target = 4 is not present in the given array so the output is 0.

Input: arr[] = [8, 9, 10, 12, 12, 12], target = 12
Output: 3
Explanation: target = 12 occurs 3 times in the given array so the output is 3.


Constraints:

1 ≤ arr.size() ≤ 106
1 ≤ arr[i] ≤ 106
1 ≤ target ≤ 106


Expected Complexities

Time Complexity: O(log n)
Auxiliary Space: O(1)


Company Tags

ZohoAmazonMakeMyTrip


Topic Tags

ArraysSearchingData StructuresAlgorithms

# Code
```cpp []
class Solution {
  public:
    int countFreq(vector<int>& arr, int target) {
        
        int l1=0 , h1=arr.size() -1;
        
        int lowerBound =  arr.size();
        while(l1<=h1){
            int mid = (l1 + h1)/2;
            if(arr[mid] >= target){ 
                h1 = mid - 1;
                lowerBound = mid;
            }
            else l1 = mid + 1;
        }
        
        
        int l2=0 , h2=arr.size() -1;
        
        int upperBound =  arr.size();
        while(l2<=h2){
            int mid = (l2 + h2)/2;
            if(arr[mid] > target){ 
                h2 = mid - 1;
                upperBound = mid;
            }
            else l2 = mid + 1;
        }
        
        return (upperBound - lowerBound);
    }
};
```

------



## Sorted and Rotated Minimum -> [GFG](https://www.geeksforgeeks.org/batch/gfg-160-problems/track/searching-gfg-160/problem/minimum-element-in-a-sorted-and-rotated-array3611)
Difficulty: Easy

A sorted array of distinct elements arr[] is rotated at some unknown point, the task is to find the minimum element in it. 

Examples:

Input: arr[] = [5, 6, 1, 2, 3, 4]
Output: 1
Explanation: 1 is the minimum element in the array.

Input: arr[] = [3, 1, 2]
Output: 1
Explanation: Here 1 is the minimum element.

Input: arr[] = [4, 2, 3]
Output: 2
Explanation: Here 2 is the minimum element.


Constraints:

1 ≤ arr.size() ≤ 106
1 ≤ arr[i] ≤ 109


Expected Complexities

Time Complexity: O(log n)
Auxiliary Space: O(1)


Company Tags

Morgan StanleyAmazonMicrosoftSamsungSnapdealAdobeTimes Internet


Topic Tags

SearchingAlgorithms

# Code
```cpp []
class Solution {
  public:
    int findMin(vector<int>& arr) {
        int l = 0 , h = arr.size() - 1;
        
        while(l<h){
            if(arr[l] < arr[h]) return arr[l];
            
            int mid = (l+h) / 2;
            
            if(arr[mid] > arr[h]) l = mid + 1;
            else h = mid;
            
        }
        
        return arr[l];
    }
};
```

------



## Search in Rotated Sorted Array -> [GFG](https://www.geeksforgeeks.org/batch/gfg-160-problems/track/searching-gfg-160/problem/search-in-a-rotated-array4618)
Difficulty: Medium

Given a sorted and rotated array arr[] of distinct elements, the task is to find the index of a target key. Return -1 if the key is not found.

Examples :

Input: arr[] = [5, 6, 7, 8, 9, 10, 1, 2, 3], key = 3
Output: 8
Explanation: 3 is found at index 8.

Input: arr[] = [3, 5, 1, 2], key = 6
Output: -1
Explanation: There is no element that has value 6.

Input: arr[] = [33, 42, 72, 99], key = 42
Output: 1
Explanation: 42 is found at index 1.


Constraints:

1 ≤ arr.size() ≤ 106
0 ≤ arr[i] ≤ 106
0 ≤ key ≤ 106


Expected Complexities

Time Complexity: O(log n)
Auxiliary Space: O(1)


Company Tags

PaytmFlipkartAmazonMicrosoftSnapdealD-E-ShawFactSetHikeMakeMyTripIntuitAdobeGoogleBankBazaarTimes Internet


Topic Tags

SearchingDivide and ConquerAlgorithms


# Code
```cpp []
class Solution {
  public:
    int search(vector<int>& arr, int key) {
        
        int l=0 , h = arr.size() -1;
        
        while(l<=h){
            int mid = (l+h) / 2;
            
            if(arr[mid] == key) return mid;
            
            if(arr[l] <= arr[mid]){
                if(arr[l] <= key && arr[mid] > key){
                    h = mid - 1;
                }else{
                    l = mid + 1;
                }
            }
            else{
                if(arr[mid] < key && arr[h] >= key){
                    l = mid + 1;
                }else{
                    h = mid - 1;
                }
            }
        }
        
        return -1;
    }
};
```

------



## K-th element of two Arrays -> [GFG](https://www.geeksforgeeks.org/batch/gfg-160-problems/track/searching-gfg-160/problem/k-th-element-of-two-sorted-array1317)
Difficulty: Medium

Given two sorted arrays a[] and b[] and an element k, the task is to find the element that would be at the kth position of the combined sorted array.

Examples :

Input: a[] = [2, 3, 6, 7, 9], b[] = [1, 4, 8, 10], k = 5
Output: 6
Explanation: The final combined sorted array would be [1, 2, 3, 4, 6, 7, 8, 9, 10]. The 5th element of this array is 6.

Input: a[] = [100, 112, 256, 349, 770], b[] = [72, 86, 113, 119, 265, 445, 892], k = 7
Output: 256
Explanation: Combined sorted array is [72, 86, 100, 112, 113, 119, 256, 265, 349, 445, 770, 892]. The 7th element of this array is 256.


Constraints:

1 <= a.size(), b.size() <= 106
1 <= k <= a.size() + b.size()
0 <= a[i], b[i] < 108


Expected Complexities

Time Complexity: O(log(min(a, b)))
Auxiliary Space: O(1)


Company Tags

FlipkartMicrosoft


Topic Tags

ArraysDivide and ConquerData StructuresAlgorithmsBinary Search


# Code
```cpp []
class Solution {
  public:
    int kthElement(vector<int>& a, vector<int>& b, int k) {
        
        int n = a.size() , m = b.size();
        int l = 0 , r = 0;
        
        vector<int> nums;
        while(l<n && r<m){
            if(a[l] <= b[r]) nums.push_back(a[l++]);
            else nums.push_back(b[r++]);
        }
        
        while(l<n) nums.push_back(a[l++]);
        
        while(r<m) nums.push_back(b[r++]);
        
        return nums[k-1];
    }
};
```

------



## Find the Frequency -> [LeetCode](https://www.geeksforgeeks.org/problems/find-the-frequency/1)
Difficulty: Easy

Given an array arr of positive integers and an integer x. Return the frequency of x in the array.

Examples :

Input: arr = [1, 1, 1, 1, 1], x = 1
Output: 5
Explanation: Frequency of 1 is 5.

Input: arr = [1, 2, 3, 3, 2, 1], x=2
Output: 2
Explanation: Frequency of 2 is 2.


Constraints:

1 <= arr.size() <= 105
1 <= arr[i] <= 105
1 <= x <= 105


Expected Complexities

Time Complexity: O(n)
Auxiliary Space: O(1)


Company Tags

Google

Topic Tags
STL


# Code
```cpp []

class Solution {
  public:
    int findFrequency(vector<int> arr, int x) {
        int count = 0;
        for(int n:arr){
            if(n == x){
                count++;
            }
        }
        
        return count;
    }
};
```

------


## Count pairs with given sum -> [GFG](https://www.geeksforgeeks.org/batch/gfg-160-problems/track/hashing-gfg-160/problem/count-pairs-with-given-sum--150253)

Difficulty: Easy

Given an array arr[] and an integer target. You have to find numbers of pairs in array arr[] which sums up to given target.

Examples:

Input: arr[] = [1, 5, 7, -1, 5], target = 6 
Output: 3
Explanation: Pairs with sum 6 are (1, 5), (7, -1) and (1, 5). 

Input: arr[] = [1, 1, 1, 1], target = 2 
Output: 6
Explanation: Pairs with sum 2 are (1, 1), (1, 1), (1, 1), (1, 1), (1, 1), (1, 1).

Input: arr[] = [10, 12, 10, 15, -1], target = 125
Output: 0


Constraints:

1 <= arr.size() <= 105
-104 <= arr[i] <= 104
1 <= target <= 104


Expected Complexities

Time Complexity: O(n)
Auxiliary Space: O(n)


Topic Tags

ArraysData StructuresHash

# Code
```cpp []
class Solution {
  public:
    int countPairs(vector<int> &arr, int target) {
        unordered_map<int,int> freq;
        
        int ans = 0;
        
        for(int i=0 ; i<arr.size() ; ++i){
            int num = arr[i];
            int need = target - num;
            if(freq.count(need)) ans+= freq[need];
            freq[num]++;
        }
        
        return ans;
    }
};
```

------

## Intersection of Two arrays with Duplicate Elements -> [GFG](https://www.geeksforgeeks.org/batch/gfg-160-problems/track/hashing-gfg-160/problem/intersection-of-two-arrays-with-duplicate-elements)
Difficulty: EasyA

Given two integer arrays a[] and b[], you have to find the intersection of the two arrays. Intersection of two arrays is said to be elements that are common in both the arrays. The intersection should not have duplicate elements and the result should contain items in any order.

Note: The driver code will sort the resulting array in increasing order before printing.

Examples:

Input: a[] = [1, 2, 1, 3, 1], b[] = [3, 1, 3, 4, 1]
Output: [1, 3]
Explanation: 1 and 3 are the only common elements and we need to print only one occurrence of common elements.

Input: a[] = [1, 1, 1], b[] = [1, 1, 1, 1, 1]
Output: [1]
Explanation: 1 is the only common element present in both the arrays.

Input: a[] = [1, 2, 3], b[] = [4, 5, 6]
Output: []
Explanation: No common element in both the arrays.


Constraints:

1 ≤ a.size(), b.size() ≤ 105
0 ≤ a[i], b[i] ≤ 105


Expected Complexities

Time Complexity: O(n + m)
Auxiliary Space: O(n)


Topic Tags

Sortingtwo-pointer-algorithmArraysHash

# Code
```cpp []
class Solution {
  public:
    vector<int> intersect(vector<int>& a, vector<int>& b) {
        
        vector<int> ans;
        set<int> s;
        set<int> s2;
        
        for(const int i:a) s.insert(i);
        for(const int i:b) s2.insert(i);
        
        for(const auto i:s2){
            if(s.count(i)) ans.push_back(i);
        }
        
        return ans;
    }
};
```

------


## Union of Arrays with Duplicates -> [GFG](https://www.geeksforgeeks.org/batch/gfg-160-problems/track/hashing-gfg-160/problem/union-of-two-arrays3538)
Difficulty: Easy

You are given two arrays a[] and b[], return the Union of both the arrays in any order.

The Union of two arrays is a collection of all distinct elements present in either of the arrays. If an element appears more than once in one or both arrays, it should be included only once in the result.

Note: Elements of a[] and b[] are not necessarily distinct.
Note that, You can return the Union in any order but the driver code will print the result in sorted order only.

Examples:

Input: a[] = [1, 2, 3, 2, 1], b[] = [3, 2, 2, 3, 3, 2]
Output: [1, 2, 3]
Explanation: Union set of both the arrays will be 1, 2 and 3.

Input: a[] = [1, 2, 3], b[] = [4, 5, 6] 
Output: [1, 2, 3, 4, 5, 6]
Explanation: Union set of both the arrays will be 1, 2, 3, 4, 5 and 6.

Input: a[] = [1, 2, 1, 1, 2], b[] = [2, 2, 1, 2, 1] 
Output: [1, 2]
Explanation: Union set of both the arrays will be 1 and 2.


Constraints:

1 ≤ a.size(), b.size() ≤ 106
0 ≤ a[i], b[i] ≤ 105


Expected Complexities

Time Complexity: O(n + m)
Auxiliary Space: O(n + m)


Company Tags

ZohoRockstand


Topic Tags

HashData StructuresAlgorithmsArrays

# Code
```cpp []
class Solution {
  public:
    vector<int> findUnion(vector<int>& a, vector<int>& b) {
        
        set<int> s(a.begin() , a.end());
        
        for(const int i:b) s.insert(i);
        
        vector<int> ans(s.begin() , s.end());
        
        return ans;
        
    }
};
```

------

## Reverse a linked list -> [GFG](https://www.geeksforgeeks.org/batch/gfg-160-problems/track/linked-list-gfg-160/problem/reverse-a-linked-list)
Difficulty: Easy

Given the head of a linked list, the task is to reverse this list and return the reversed head.

Examples:

Input: head: 1 -> 2 -> 3 -> 4 -> NULL
Output: head: 4 -> 3 -> 2 -> 1 -> NULL
Explanation:

Input: head: 2 -> 7 -> 10 -> 9 -> 8 -> NULL
Output: head: 8 -> 9 -> 10 -> 7 -> 2 -> NULL
Explanation:

Input: head: 2 -> NULL
Output: 2 -> NULL
Explanation:

Constraints:

1 <= number of nodes, data of nodes <= 105


Expected Complexities

Time Complexity: O(n)
Auxiliary Space: O(1)


Company Tags

PaytmVMWareZohoAccoliteAmazonMicrosoftSamsungSnapdealD-E-ShawMakeMyTripTeradataWalmartGoldman SachsIntuitAdobeSAP LabsTejas NetworkCiscoQualcommCognizantMahindra ComvivaIgniteWorld


Topic Tags

Linked ListData Structures

# Code
```cpp []
/* Linked List Node structure:

struct Node
{
    int data;
    struct Node *next;
}

*/

class Solution {
  public:
    Node* reverseList(struct Node* head) {
        Node* temp = head;
        stack<Node*> st;
        while(temp->next){
            st.push(temp);
            temp = temp->next;
        }
        
        head = temp;
        
        while(!st.empty()){
            temp->next = st.top(); st.pop();
            temp = temp->next;
        }
        
        temp->next = nullptr;
        
        return head;
    }
};
```

------


## Remove all occurences of duplicates in a linked list -> [GFG](https://www.geeksforgeeks.org/problems/remove-all-occurences-of-duplicates-in-a-linked-list/1)
Difficulty: Medium

Given a sorted linked list, delete all nodes that have duplicate numbers (all occurrences), leaving only numbers that appear once in the original list, and return the head of the modified linked list. 

Examples:

Input: Linked List = 23->28->28->35->49->49->53->53
Output: 23 35
Explanation: 

The duplicate numbers are 28, 49 and 53 which are removed from the list.
Input: Linked List = 11->11->11->11->75->75
Output: Empty list
Explanation: 

All the nodes in the linked list have duplicates. Hence the resultant list would be empty.

Expected Time Complexity: O(n)

Expected Auxiliary Space: O(1)


Constraints:

list.data>0
1 ≤ size(list) ≤ 105


Company Tags

Microsoft


Topic Tags

Linked ListData Structures

# Code
```cpp []
// User function Template for C++

/* Linked List node structure

struct Node {
    int data;
    struct Node *next;
};

*/

class Solution {
  public:
    Node* removeAllDuplicates(struct Node* head) {
        Node* dummy = new Node(-1);
        dummy->next = head;
        Node* prev = dummy;
        Node *cur = head;
        
        while(cur){
            while(cur->next && prev->next->data == cur->next->data)
                cur = cur->next;
            if(prev->next == cur)
                prev = cur;
            else{
                prev->next = cur->next;
            }
            cur = cur->next;
        }
        
        return dummy->next;
    }
};
```

------


## Rotate a Linked List -> [GFG](https://www.geeksforgeeks.org/batch/gfg-160-problems/track/linked-list-gfg-160/problem/rotate-a-linked-list)
Difficulty: Medium

Given the head of a singly linked list, your task is to left rotate the linked list k times.

Examples:

Input: head = 10 -> 20 -> 30 -> 40 -> 50, k = 4
Output: 50 -> 10 -> 20 -> 30 -> 40
Explanation:
Rotate 1: 20 -> 30 -> 40 -> 50 -> 10
Rotate 2: 30 -> 40 -> 50 -> 10 -> 20
Rotate 3: 40 -> 50 -> 10 -> 20 -> 30
Rotate 4: 50 -> 10 -> 20 -> 30 -> 40


Input: head = 10 -> 20 -> 30 -> 40 , k = 6
Output: 30 -> 40 -> 10 -> 20 
 
Constraints:

1 <= number of nodes <= 105
0 <= k <= 109
0 <= data of node <= 109


Expected Complexities

Time Complexity: O(n)
Auxiliary Space: O(1)


Company Tags

AccoliteAmazonMicrosoftMakeMyTrip


Topic Tags

Linked ListData Structures

# Code
```cpp []
/*
struct Node {
    int data;
    struct Node *next;
    Node(int x) {
        data = x;
        next = NULL;
    }
} */

class Solution {
  public:
    Node* rotate(Node* head, int k) {
       if(k == 0 || head == nullptr) return head;
        
       Node* cur = head;
       
       int len = 1;
       
       while(cur->next){
           len++;
           cur = cur->next;
       }
       
       k %= len;
       
       if(k == 0) return head;
       
       cur->next = head;
       cur = head;
       
       for(int i=1 ; i<k ; ++i){
           cur = cur->next;
       }
       
       head = cur->next;
       cur->next = nullptr;
       
       
       return head;
       
       
    }
};
```

------

## Merge two sorted linked lists ->  [GFG](https://www.geeksforgeeks.org/batch/gfg-160-problems/track/linked-list-gfg-160/problem/merge-two-sorted-linked-lists)
Difficulty: Medium

Given the head of two sorted linked lists consisting of nodes respectively. The task is to merge both lists and return the head of the sorted merged list.

Examples:

Input: head1 = 5 -> 10 -> 15 -> 40, head2 = 2 -> 3 -> 20
Output: 2 -> 3 -> 5 -> 10 -> 15 -> 20 -> 40
Explanation:

Input: head1 = 1 -> 1, head2 = 2 -> 4
Output: 1 -> 1 -> 2 -> 4
Explanation:

Constraints:
1 <= no. of nodes<= 103
0 <= node->data <= 105


Company Tags


ZohoFlipkartAccoliteAmazonMicrosoftSamsungFactSetMakeMyTripOracleBrocadeSynopsysOATS SystemsBelzabar


Topic Tags

Linked ListData Structures


# Code
```cpp []
/* Link list Node
struct Node {
  int data;
  struct Node *next;

  Node(int x) {
    data = x;
    next = NULL;
  }
};
*/
class Solution {
  public:
    Node* sortedMerge(Node* head1, Node* head2) {
        if(!head1) return head2;
        if(!head2) return head1;
        
        if(head1->data < head2->data){
            head1->next = sortedMerge(head1->next , head2);
            return head1;
        }
        else{
            head2->next = sortedMerge(head1 , head2->next);
            return head2;
        }
    }
};
```

------


## Level order traversal -> [GFG](https://www.geeksforgeeks.org/batch/gfg-160-problems/track/tree-gfg-160/problem/level-order-traversal)
Difficulty: Easy

Given a root of a binary tree with n nodes, the task is to find its level order traversal. Level order traversal of a tree is breadth-first traversal for the tree.

Examples:

Input: root[] = [1, 2, 3]

Output: [[1], [2, 3]]
Input: root[] = [10, 20, 30, 40, 50]

Output: [[10], [20, 30], [40, 50]]
Input: root[] = [1, 3, 2, N, N, N, 4, 6, 5]

Output: [[1], [3, 2], [4], [6, 5]]


Constraints:

1 ≤ number of nodes ≤ 105
0 ≤ node->data ≤ 109


Expected Complexities

Time Complexity: O(n)
Auxiliary Space: O(n)


Company Tags

FlipkartMorgan StanleyAccoliteAmazonMicrosoftSamsungD-E-ShawOla CabsPayuAdobeCiscoQualcomm


Topic Tags

TreeData Structures


# Code
```cpp []
/* A binary tree Node
class Node {
  public:
    int data;
    Node* left;
    Node* right;

    // Constructor
    Node(int val) {
        data = val;
        left = nullptr;
        right = nullptr;
    }
};
*/

class Solution {
  public:
    vector<vector<int>> levelOrder(Node *root) {
        vector<vector<int>> ans;
        queue<Node*> q;
        q.push(root);
        
        while(!q.empty()){
            int n = q.size();
            vector<int> level;
            for(int i=0 ; i<n ; ++i){
                Node* cur = q.front(); q.pop();
                level.push_back(cur->data);
                if(cur->left) q.push(cur->left);
                if(cur->right) q.push(cur->right);
            }
            
            ans.push_back(level);
        }
        
        return ans;
        
    }
};
```

------


## Height of Binary Tree -> [GFG](https://www.geeksforgeeks.org/batch/gfg-160-problems/track/tree-gfg-160/problem/height-of-binary-tree)
Difficulty: Easy

Given a binary tree, find its height.

The height of a tree is defined as the number of edges on the longest path from the root to a leaf node. A leaf node is a node that does not have any children.

Examples:

Input: root[] = [12, 8, 18, 5, 11] 
 
Output: 2
Explanation: One of the longest path from the root (node 12) goes through node 8 to node 5, which has 2 edges.


Input: root[] = [1, 2, 3, 4, N, N, 5, N, N, 6, 7]  

Output: 3
Explanation: The longest path from the root (node 1) to a leaf node 6 with 3 edge.



Constraints:

1 <= number of nodes <= 105
0 <= node->data <= 105


Expected Complexities

Time Complexity: O(n)
Auxiliary Space: O(n)


Company Tags

VMWareZohoAmazonMicrosoftSnapdealD-E-ShawFactSetMakeMyTripTeradataSynopsysCouponDuniaCadence IndiaMonotype SolutionsFreeCharge


Topic Tags

TreeData Structures

# Code
```cpp []
/*
class Node {
public:
    int data;
    Node* left;
    Node* right;

    Node(int val) {
        data = val;
        left = right = NULL;
    }
};
*/
class Solution {
  public:
    int height(Node* node) {
        int h = -1;
        queue<Node*> q;
        q.push(node);
        
        while(!q.empty()){
            int n = q.size();
            for(int i=0 ; i<n ; ++i ){
                Node* cur = q.front(); q.pop();
                if(cur->left) q.push(cur->left);
                if(cur->right) q.push(cur->right);
            }
            h++;
        }
        
        return h;
    }
};
```

------


## Count Inversions -> [GFG](https://www.geeksforgeeks.org/batch/gfg-160-problems/track/sorting-gfg-160/problem/inversion-of-array-1587115620)
Difficulty: Medium

Given an array of integers arr[]. You have to find the Inversion Count of the array. 
Note : Inversion count is the number of pairs of elements (i, j) such that i < j and arr[i] > arr[j].

Examples:

Input: arr[] = [2, 4, 1, 3, 5]
Output: 3
Explanation: The sequence 2, 4, 1, 3, 5 has three inversions (2, 1), (4, 1), (4, 3).

Input: arr[] = [2, 3, 4, 5, 6]
Output: 0
Explanation: As the sequence is already sorted so there is no inversion count.

Input: arr[] = [10, 10, 10]
Output: 0
Explanation: As all the elements of array are same, so there is no inversion count.


Constraints:

1 ≤ arr.size() ≤ 105
1 ≤ arr[i] ≤ 104


Expected Complexities

Time Complexity: O(n log n)
Auxiliary Space: O(n)


Company Tags

FlipkartAmazonMicrosoftMakeMyTripAdobeBankBazaarMyntra


Topic Tags

ArraysDivide and ConquerSortingData StructuresAlgorithms



# Code
```cpp []
class Solution {
  private:
    int conquer(vector<int> &arr , int l , int m , int r){
        int res = 0;
        int i=l , j=m+1;
        vector<int> temp;
        while(i<=m && j<=r){
            if(arr[i] <= arr[j]) temp.push_back(arr[i++]);
            else{
                res += (m - i + 1);
                temp.push_back(arr[j++]);
            }
        }
        
        while(i<=m) temp.push_back(arr[i++]);
        while(j<=r) temp.push_back(arr[j++]);
        
        for(int k=l ; k<=r ; ++k){
            arr[k] = temp[k-l];
        }
        
        return res;
        
    }
  
    int divide(vector<int> &arr , int l , int r){
        int res = 0;
        if(l<r){
            int m = (l + r) / 2;
            res += divide(arr,l , m);
            res += divide(arr,m+1 , r);
            res += conquer(arr,l,m,r);
        }
        return res;
    }
  public:
    int inversionCount(vector<int> &arr) {
        int n = arr.size();
        return divide(arr , 0, n-1);
    }
};
```

------



## Longest Increasing Subsequence
Difficulty: Medium

Given an array arr[] of non-negative integers, the task is to find the length of the Longest Strictly Increasing Subsequence (LIS).

A subsequence is strictly increasing if each element in the subsequence is strictly less than the next element.

Examples:

Input: arr[] = [5, 8, 3, 7, 9, 1]
Output: 3
Explanation: The longest strictly increasing subsequence could be [5, 7, 9], which has a length of 3.

Input: arr[] = [0, 8, 4, 12, 2, 10, 6, 14, 1, 9, 5, 13, 3, 11, 7, 15]
Output: 6
Explanation: One of the possible longest strictly increasing subsequences is [0, 2, 6, 9, 13, 15], which has a length of 6.

Input: arr[] = [3, 10, 2, 1, 20]
Output: 3
Explanation: The longest strictly increasing subsequence could be [3, 10, 20], which has a length of 3.


Constraints:

1 ≤ arr.size() ≤ 103
0 ≤ arr[i] ≤ 106


Expected Complexities

Time Complexity: O(n log n)
Auxiliary Space: O(n)


Company Tags

PaytmAmazonMicrosoftOYO RoomsSamsungBankBazaar


Topic Tags

Dynamic ProgrammingBinary SearchAlgorithms


# Code
```cpp []
class Solution {
  public:
    int lis(vector<int>& arr) {
       int n = arr.size();
       vector<int> res(n , 1 );
       int maxx = 1;
       for(int i=1 ; i<n ; ++i ){
           for(int j=0 ; j<i ; ++j){
               if(arr[i] > arr[j] ){
                   res[i] = max(res[i] , res[j] + 1); 
                   maxx = max(maxx , res[i]);
               }
           }
       }
       
       return maxx;
    }
};
```

------

