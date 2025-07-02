


------------------------------------
# *LEETCODE* - **july-2025**
------------------------------------


# 3330. Find the Original Typed String I -> [Leetcode](https://leetcode.com/problems/find-the-original-typed-string-i/description/)

Easy

Alice is attempting to type a specific string on her computer. However, she tends to be clumsy and may press a key for too long, resulting in a character being typed multiple times.

Although Alice tried to focus on her typing, she is aware that she may still have done this at most once.

You are given a string word, which represents the final output displayed on Alice's screen.

Return the total number of possible original strings that Alice might have intended to type.

 

Example 1:

Input: word = "abbcccc"

Output: 5

Explanation:

The possible strings are: "abbcccc", "abbccc", "abbcc", "abbc", and "abcccc".

Example 2:

Input: word = "abcd"

Output: 1

Explanation:

The only possible string is "abcd".

Example 3:

Input: word = "aaaa"

Output: 4

 

Constraints:

1 <= word.length <= 100
word consists only of lowercase English letters.

# Code
```cpp []
class Solution {
public:
    int possibleStringCount(string word) {
        int ans = 1;

        for(int i=1 ; i<word.length() ; ++i){
            if(word[i] == word[i-1]) ans++;
        }

        return ans;
    }
};
```


-----

# 344. Reverse String -> [LeetCode](https://leetcode.com/problems/reverse-string/description/)

Easy

Write a function that reverses a string. The input string is given as an array of characters s.

You must do this by modifying the input array in-place with O(1) extra memory.

 

Example 1:

Input: s = ["h","e","l","l","o"]
Output: ["o","l","l","e","h"]


Example 2:

Input: s = ["H","a","n","n","a","h"]
Output: ["h","a","n","n","a","H"]
 

Constraints:

1 <= s.length <= 105
s[i] is a printable ascii character.

# Code
```cpp []
class Solution {
public:
    void reverseString(vector<char>& s) {
      int i=0 , j = s.size() -1;

      while(i<j){
        char c = s[i];
        s[i++] = s[j];
        s[j--] = c;
      }
    }
};
```

------

# 151. Reverse Words in a String -> [LeetCode](https://leetcode.com/problems/reverse-words-in-a-string/description/)
 
Medium

Given an input string s, reverse the order of the words.

A word is defined as a sequence of non-space characters. The words in s will be separated by at least one space.

Return a string of the words in reverse order concatenated by a single space.

Note that s may contain leading or trailing spaces or multiple spaces between two words. The returned string should only have a single space separating the words. Do not include any extra spaces.

 

Example 1:

Input: s = "the sky is blue"
Output: "blue is sky the"


Example 2:

Input: s = "  hello world  "
Output: "world hello"
Explanation: Your reversed string should not contain leading or trailing spaces.


Example 3:

Input: s = "a good   example"
Output: "example good a"
Explanation: You need to reduce multiple spaces between two words to a single space in the reversed string.
 

Constraints:

1 <= s.length <= 104
s contains English letters (upper-case and lower-case), digits, and spaces ' '.
There is at least one word in s.
 

Follow-up: If the string data type is mutable in your language, can you solve it in-place with O(1) extra space?

# Code
```cpp []
class Solution {
public:
    string reverseWords(string s) {
        vector<string> words;

        string word;

        for(const char c:s){
            if(c != ' '){
                word+=c;
            }else if(c == ' ' && !word.empty() ){
                words.push_back(word);
                word.clear();
            }
        }

        if(!word.empty()){
           words.push_back(word);
           word.clear();
        }

        string ans;

        for(int i=words.size() - 1 ; i>=0 ; --i){
            ans+=words[i];
            if( i != 0) ans+=' ';
        }

        return ans;


    }
};
```


--------------------


# 3333. Find the Original Typed String II -> LeetCode

Hard

Alice is attempting to type a specific string on her computer. However, she tends to be clumsy and may press a key for too long, resulting in a character being typed multiple times.

You are given a string word, which represents the final output displayed on Alice's screen. You are also given a positive integer k.

Return the total number of possible original strings that Alice might have intended to type, if she was trying to type a string of size at least k.

Since the answer may be very large, return it modulo 109 + 7.

 

Example 1:

Input: word = "aabbccdd", k = 7

Output: 5

Explanation:

The possible strings are: "aabbccdd", "aabbccd", "aabbcdd", "aabccdd", and "abbccdd".

Example 2:

Input: word = "aabbccdd", k = 8

Output: 1

Explanation:

The only possible string is "aabbccdd".

Example 3:

Input: word = "aaabbb", k = 3

Output: 8

 

Constraints:

1 <= word.length <= 5 * 105
word consists only of lowercase English letters.
1 <= k <= 2000


# Code
```cpp []
class Solution {
 public:
  int possibleStringCount(string word, int k) {
    const vector<int> groups = getConsecutiveLetters(word);
    const int totalCombinations =
        accumulate(groups.begin(), groups.end(), 1L,
                   [](long acc, int group) { return acc * group % kMod; });
    if (k <= groups.size())
      return totalCombinations;

    
    vector<int> dp(k);
    dp[0] = 1;  

    for (int i = 0; i < groups.size(); ++i) {
      vector<int> newDp(k);
      int windowSum = 0;
      int group = groups[i];
      for (int j = i; j < k; ++j) {
        newDp[j] = (newDp[j] + windowSum) % kMod;
        windowSum = (windowSum + dp[j]) % kMod;
        if (j >= group)
          windowSum = (windowSum - dp[j - group] + kMod) % kMod;
      }
      dp = std::move(newDp);
    }

    const int invalidCombinations =
        accumulate(dp.begin(), dp.end(), 0,
                   [](int acc, int count) { return (acc + count) % kMod; });
    return (totalCombinations - invalidCombinations + kMod) % kMod;
  }

 private:
  static constexpr int kMod = 1'000'000'007;

  
  vector<int> getConsecutiveLetters(const string& word) {
    vector<int> groups;
    int group = 1;
    for (int i = 1; i < word.length(); ++i)
      if (word[i] == word[i - 1]) {
        ++group;
      } else {
        groups.push_back(group);
        group = 1;
      }
    groups.push_back(group);
    return groups;
  }
};
```

--------



