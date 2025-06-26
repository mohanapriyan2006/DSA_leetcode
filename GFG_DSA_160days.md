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


