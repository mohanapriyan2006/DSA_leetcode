
--------------------------------------
# *LEETCODE* - **july-2025**
--------------------------------------


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


