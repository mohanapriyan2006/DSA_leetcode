
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


# 3333. Find the Original Typed String II -> [LeetCode](https://leetcode.com/problems/find-the-original-typed-string-ii/description)

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

# 83. Remove Duplicates from Sorted List -> [LeetCode](https://leetcode.com/problems/remove-duplicates-from-sorted-list/description/)

Easy

Given the head of a sorted linked list, delete all duplicates such that each element appears only once. Return the linked list sorted as well.

 

Example 1:


Input: head = [1,1,2]
Output: [1,2]


Example 2:


Input: head = [1,1,2,3,3]
Output: [1,2,3]
 

Constraints:

The number of nodes in the list is in the range [0, 300].
-100 <= Node.val <= 100
The list is guaranteed to be sorted in ascending order.

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
    ListNode* deleteDuplicates(ListNode* head) {
        ListNode* temp = head;
        
        if(head == nullptr) return head;
        
        while(temp != nullptr){
            while(temp->next && temp->val == temp->next->val){
                temp->next = temp->next->next;
            }
            temp = temp->next;
        }
        
        return head;
    }
};
```


-----------------


# 876. Middle of the Linked List -> [LeetCode](https://leetcode.com/problems/middle-of-the-linked-list/description/)

Easy

Given the head of a singly linked list, return the middle node of the linked list.

If there are two middle nodes, return the second middle node.

 

Example 1:


Input: head = [1,2,3,4,5]
Output: [3,4,5]
Explanation: The middle node of the list is node 3.


Example 2:


Input: head = [1,2,3,4,5,6]
Output: [4,5,6]
Explanation: Since the list has two middle nodes with values 3 and 4, we return the second one.
 

Constraints:

The number of nodes in the list is in the range [1, 100].
1 <= Node.val <= 100

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
    ListNode* middleNode(ListNode* head) {
        ListNode* slow = head;
        ListNode* fast = head;

        while( fast != nullptr && fast->next != nullptr){
            slow = slow->next;
            fast = fast->next->next;
        }

        return slow;
    }
};
```

---------



# 2095. Delete the Middle Node of a Linked List -> [LeetCode](https://leetcode.com/problems/delete-the-middle-node-of-a-linked-list/description/)

Medium

You are given the head of a linked list. Delete the middle node, and return the head of the modified linked list.

The middle node of a linked list of size n is the ⌊n / 2⌋th node from the start using 0-based indexing, where ⌊x⌋ denotes the largest integer less than or equal to x.

For n = 1, 2, 3, 4, and 5, the middle nodes are 0, 1, 1, 2, and 2, respectively.
 

Example 1:


Input: head = [1,3,4,7,1,2,6]
Output: [1,3,4,1,2,6]
Explanation:
The above figure represents the given linked list. The indices of the nodes are written below.
Since n = 7, node 3 with value 7 is the middle node, which is marked in red.
We return the new list after removing this node. 


Example 2:


Input: head = [1,2,3,4]
Output: [1,2,4]
Explanation:
The above figure represents the given linked list.
For n = 4, node 2 with value 3 is the middle node, which is marked in red.


Example 3:


Input: head = [2,1]
Output: [2]
Explanation:
The above figure represents the given linked list.
For n = 2, node 1 with value 1 is the middle node, which is marked in red.
Node 0 with value 2 is the only node remaining after removing node 1.
 

Constraints:

The number of nodes in the list is in the range [1, 105].
1 <= Node.val <= 105

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
    ListNode* deleteMiddle(ListNode* head) {

        if( head == nullptr || head->next == nullptr ){
            return nullptr;
        }

        int c = 0;

        ListNode* temp = head;

        while(temp != nullptr){
            c++;
            temp = temp->next;
        }

        int mid = c/2;
        ListNode* cur = head;
        for(int i=1 ; i<mid ; ++i){
            cur = cur->next;
        }

        ListNode* toDel = cur->next;
        cur->next = cur->next->next;
        delete toDel;

        return head;
    }
};
```

-----


# 206. Reverse Linked List -> [LeetCode](https://leetcode.com/problems/reverse-linked-list/description/)

Easy

Given the head of a singly linked list, reverse the list, and return the reversed list.

 

Example 1:


Input: head = [1,2,3,4,5]
Output: [5,4,3,2,1]


Example 2:


Input: head = [1,2]
Output: [2,1]


Example 3:

Input: head = []
Output: []
 

Constraints:

The number of nodes in the list is the range [0, 5000].
-5000 <= Node.val <= 5000
 

Follow up: A linked list can be reversed either iteratively or recursively. Could you implement both?

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
    ListNode* reverseList(ListNode* head) {
        ListNode* prev = nullptr;
         while(head != nullptr){
            ListNode* next = head->next;
            head->next = prev;
            prev = head;
            head = next;
         }

         return prev;
    }
};
```

-----------

# 3304. Find the K-th Character in String Game I -> [LeetCode](https://leetcode.com/problems/find-the-k-th-character-in-string-game-i/description/)

Easy

Alice and Bob are playing a game. Initially, Alice has a string word = "a".

You are given a positive integer k.

Now Bob will ask Alice to perform the following operation forever:

Generate a new string by changing each character in word to its next character in the English alphabet, and append it to the original word.
For example, performing the operation on "c" generates "cd" and performing the operation on "zb" generates "zbac".

Return the value of the kth character in word, after enough operations have been done for word to have at least k characters.

Note that the character 'z' can be changed to 'a' in the operation.

 

Example 1:

Input: k = 5

Output: "b"

Explanation:

Initially, word = "a". We need to do the operation three times:

Generated string is "b", word becomes "ab".
Generated string is "bc", word becomes "abbc".
Generated string is "bccd", word becomes "abbcbccd".


Example 2:

Input: k = 10

Output: "c"

 

Constraints:

1 <= k <= 500

# Code
```cpp []
class Solution {
public:
    char kthCharacter(unsigned k) {
        return 'a' + popcount(k-1);
    }
};
```


-----


# 20. Valid Parentheses -> [LeetCode](https://leetcode.com/problems/valid-parentheses/description/)

Easy

Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

Open brackets must be closed by the same type of brackets.
Open brackets must be closed in the correct order.
Every close bracket has a corresponding open bracket of the same type.
 

Example 1:

Input: s = "()"

Output: true

Example 2:

Input: s = "()[]{}"

Output: true

Example 3:

Input: s = "(]"

Output: false

Example 4:

Input: s = "([])"

Output: true

 

Constraints:

1 <= s.length <= 104
s consists of parentheses only '()[]{}'.

# Code
```cpp []
class Solution {
public:
    bool isValid(string s) {

        stack<char> st;

        for(const char c:s){
           if(!st.empty()){
            if(st.top() == '(' && c == ')'){
                st.pop();
            }
            else if(st.top() == '{' && c == '}'){
                st.pop();
            }
            else if(st.top() == '[' && c == ']'){
                st.pop();
            }else{
                st.push(c);
            }
           }else{
            st.push(c);
           }

        }

        return st.empty();
    }
};
```

--------


# 3307. Find the K-th Character in String Game II -> [LeetCode](https://leetcode.com/problems/find-the-k-th-character-in-string-game-ii/description/)

Hard

Alice and Bob are playing a game. Initially, Alice has a string word = "a".

You are given a positive integer k. You are also given an integer array operations, where operations[i] represents the type of the ith operation.

Now Bob will ask Alice to perform all operations in sequence:

If operations[i] == 0, append a copy of word to itself.
If operations[i] == 1, generate a new string by changing each character in word to its next character in the English alphabet, and append it to the original word. For example, performing the operation on "c" generates "cd" and performing the operation on "zb" generates "zbac".
Return the value of the kth character in word after performing all the operations.

Note that the character 'z' can be changed to 'a' in the second type of operation.

 

Example 1:

Input: k = 5, operations = [0,0,0]

Output: "a"

Explanation:

Initially, word == "a". Alice performs the three operations as follows:

Appends "a" to "a", word becomes "aa".
Appends "aa" to "aa", word becomes "aaaa".
Appends "aaaa" to "aaaa", word becomes "aaaaaaaa".


Example 2:

Input: k = 10, operations = [0,1,0,1]

Output: "b"

Explanation:

Initially, word == "a". Alice performs the four operations as follows:

Appends "a" to "a", word becomes "aa".
Appends "bb" to "aa", word becomes "aabb".
Appends "aabb" to "aabb", word becomes "aabbaabb".
Appends "bbccbbcc" to "aabbaabb", word becomes "aabbaabbbbccbbcc".
 

Constraints:

1 <= k <= 1014
1 <= operations.length <= 100
operations[i] is either 0 or 1.
The input is generated such that word has at least k characters after all operations.

# Code
```cpp []
class Solution {
 public:
  char kthCharacter(long long k, vector<int>& operations) {
    const int operationsCount = ceil(log2(k));
    int increases = 0;

    for (int i = operationsCount - 1; i >= 0; --i) {
      const long halfSize = 1L << i;
      if (k > halfSize) {
        k -= halfSize;
        increases += operations[i];
      }
    }

    return 'a' + increases % 26;
  }
};
```

------



# 155. Min Stack -> [LeetCode](https://leetcode.com/problems/min-stack/description/)

Medium

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

Implement the MinStack class:

MinStack() initializes the stack object.
void push(int val) pushes the element val onto the stack.
void pop() removes the element on the top of the stack.
int top() gets the top element of the stack.
int getMin() retrieves the minimum element in the stack.
You must implement a solution with O(1) time complexity for each function.

 

Example 1:

Input
["MinStack","push","push","push","getMin","pop","top","getMin"]
[[],[-2],[0],[-3],[],[],[],[]]

Output
[null,null,null,null,-3,null,0,-2]

Explanation
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin(); // return -3
minStack.pop();
minStack.top();    // return 0
minStack.getMin(); // return -2
 

Constraints:

-231 <= val <= 231 - 1
Methods pop, top and getMin operations will always be called on non-empty stacks.
At most 3 * 104 calls will be made to push, pop, top, and getMin.

# Code
```cpp []
class MinStack {
public:
    
    void push(int val) {
        if(st.empty()) st.emplace(val,val);
        else{
            int mini = min(val,st.top().second);
            st.emplace(val,mini);
        }
    }
    
    void pop() {
        st.pop();
    }
    
    int top() {
        return st.top().first;
    }
    
    int getMin() {
        return st.top().second;
    }

private:
    stack<pair<int,int>> st;
};

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack* obj = new MinStack();
 * obj->push(val);
 * obj->pop();
 * int param_3 = obj->top();
 * int param_4 = obj->getMin();
 */
```


------------

# 225. Implement Stack using Queues -> [LeetCode](https://leetcode.com/problems/implement-stack-using-queues/description)

Easy

Implement a last-in-first-out (LIFO) stack using only two queues. The implemented stack should support all the functions of a normal stack (push, top, pop, and empty).

Implement the MyStack class:

void push(int x) Pushes element x to the top of the stack.
int pop() Removes the element on the top of the stack and returns it.
int top() Returns the element on the top of the stack.
boolean empty() Returns true if the stack is empty, false otherwise.
Notes:

You must use only standard operations of a queue, which means that only push to back, peek/pop from front, size and is empty operations are valid.
Depending on your language, the queue may not be supported natively. You may simulate a queue using a list or deque (double-ended queue) as long as you use only a queue's standard operations.
 

Example 1:

Input
["MyStack", "push", "push", "top", "pop", "empty"]
[[], [1], [2], [], [], []]
Output
[null, null, null, 2, 2, false]

Explanation
MyStack myStack = new MyStack();
myStack.push(1);
myStack.push(2);
myStack.top(); // return 2
myStack.pop(); // return 2
myStack.empty(); // return False
 

Constraints:

1 <= x <= 9
At most 100 calls will be made to push, pop, top, and empty.
All the calls to pop and top are valid.
 

Follow-up: Can you implement the stack using only one queue?

# Code
```cpp []
class MyStack {
public:
    
    void push(int x) {
        st.push(x);
        for(int i=0 ; i<st.size() - 1 ; ++i){
            st.push(st.front());
            st.pop();
        }
    }
    
    int pop() {
        int n = st.front();
        st.pop();
        return n;
    }
    
    int top() {
        return st.front();
    }
    
    bool empty() {
        return st.empty();
    }

private:
    queue<int> st;
};

/**
 * Your MyStack object will be instantiated and called as such:
 * MyStack* obj = new MyStack();
 * obj->push(x);
 * int param_2 = obj->pop();
 * int param_3 = obj->top();
 * bool param_4 = obj->empty();
 */
```

----

# 1394. Find Lucky Integer in an Array -> [LeetCode](https://leetcode.com/problems/find-lucky-integer-in-an-array/description/)

Easy

Given an array of integers arr, a lucky integer is an integer that has a frequency in the array equal to its value.

Return the largest lucky integer in the array. If there is no lucky integer return -1.

 

Example 1:

Input: arr = [2,2,3,4]
Output: 2
Explanation: The only lucky number in the array is 2 because frequency[2] == 2.


Example 2:

Input: arr = [1,2,2,3,3,3]
Output: 3
Explanation: 1, 2 and 3 are all lucky numbers, return the largest of them.


Example 3:

Input: arr = [2,2,2,3,3]
Output: -1
Explanation: There are no lucky numbers in the array.
 

Constraints:

1 <= arr.length <= 500
1 <= arr[i] <= 500

# Code
```cpp []
class Solution {
public:
    int findLucky(vector<int>& arr) {

        int ans = -1;

        unordered_map<int,int> freq;
        for(const int num:arr){
            freq[num]++;
        }

        for(auto it:freq){
            if(it.first == it.second) ans = max(it.first,ans);
        }

        return ans;
    }
};
```

-----------

# 169. Majority Element -> [LeetCode](https://leetcode.com/problems/majority-element/description/)

Easy

### amazon

Given an array nums of size n, return the majority element.

The majority element is the element that appears more than ⌊n / 2⌋ times. You may assume that the majority element always exists in the array.

 

Example 1:

Input: nums = [3,2,3]
Output: 3
Example 2:

Input: nums = [2,2,1,1,1,2,2]
Output: 2
 

Constraints:

n == nums.length
1 <= n <= 5 * 104
-109 <= nums[i] <= 109
 

Follow-up: Could you solve the problem in linear time and in O(1) space?

# Code
```cpp []
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int x = nums.size()/2;
        unordered_map<int,int> freq;
        for(const int num:nums){
            freq[num]++;
        }

        int ans = -1;

        for(auto it:freq){
            if(it.second > x) ans = it.first;
        }

        return ans;
    }
};
```

-----



# 1865. Finding Pairs With a Certain Sum -> [LeetCode](https://leetcode.com/problems/finding-pairs-with-a-certain-sum/description)

Medium

You are given two integer arrays nums1 and nums2. You are tasked to implement a data structure that supports queries of two types:

Add a positive integer to an element of a given index in the array nums2.
Count the number of pairs (i, j) such that nums1[i] + nums2[j] equals a given value (0 <= i < nums1.length and 0 <= j < nums2.length).
Implement the FindSumPairs class:

FindSumPairs(int[] nums1, int[] nums2) Initializes the FindSumPairs object with two integer arrays nums1 and nums2.
void add(int index, int val) Adds val to nums2[index], i.e., apply nums2[index] += val.
int count(int tot) Returns the number of pairs (i, j) such that nums1[i] + nums2[j] == tot.
 

Example 1:

Input
["FindSumPairs", "count", "add", "count", "count", "add", "add", "count"]
[[[1, 1, 2, 2, 2, 3], [1, 4, 5, 2, 5, 4]], [7], [3, 2], [8], [4], [0, 1], [1, 1], [7]]
Output
[null, 8, null, 2, 1, null, null, 11]

Explanation

FindSumPairs findSumPairs = new FindSumPairs([1, 1, 2, 2, 2, 3], [1, 4, 5, 2, 5, 4]);
findSumPairs.count(7);  // return 8; pairs (2,2), (3,2), (4,2), (2,4), (3,4), (4,4) make 2 + 5 and pairs (5,1), (5,5) make 3 + 4
findSumPairs.add(3, 2); // now nums2 = [1,4,5,4,5,4]
findSumPairs.count(8);  // return 2; pairs (5,2), (5,4) make 3 + 5
findSumPairs.count(4);  // return 1; pair (5,0) makes 3 + 1
findSumPairs.add(0, 1); // now nums2 = [2,4,5,4,5,4]
findSumPairs.add(1, 1); // now nums2 = [2,5,5,4,5,4]
findSumPairs.count(7);  // return 11; pairs (2,1), (2,2), (2,4), (3,1), (3,2), (3,4), (4,1), (4,2), (4,4) make 2 + 5 and pairs (5,3), (5,5) make 3 + 4
 

Constraints:

1 <= nums1.length <= 1000
1 <= nums2.length <= 105
1 <= nums1[i] <= 109
1 <= nums2[i] <= 105
0 <= index < nums2.length
1 <= val <= 105
1 <= tot <= 109
At most 1000 calls are made to add and count each.

# Code
```cpp []
class FindSumPairs {
 public:
  FindSumPairs(vector<int>& nums1, vector<int>& nums2)
      : nums1(nums1), nums2(nums2) {
    for (const int num : nums2)
      ++count2[num];
  }

  void add(int index, int val) {
    --count2[nums2[index]];
    nums2[index] += val;
    ++count2[nums2[index]];
  }

  int count(int tot) {
    int ans = 0;
    for (const int num : nums1) {
      const int target = tot - num;
      if (const auto it = count2.find(target); it != count2.cend())
        ans += it->second;
    }
    return ans;
  }

 private:
  vector<int> nums1;
  vector<int> nums2;
  unordered_map<int, int> count2;
};
```

-------

# I1353. Maximum Number of Events That Can Be Attended -> [LeetCode](https://leetcode.com/problems/maximum-number-of-events-that-can-be-attended/description/)

Topics

You are given an array of events where events[i] = [startDayi, endDayi]. Every event i starts at startDayi and ends at endDayi.

You can attend an event i at any day d where startTimei <= d <= endTimei. You can only attend one event at any time d.

Return the maximum number of events you can attend.

 

Example 1:


Input: events = [[1,2],[2,3],[3,4]]
Output: 3
Explanation: You can attend all the three events.
One way to attend them all is as shown.
Attend the first event on day 1.
Attend the second event on day 2.
Attend the third event on day 3.

Example 2:

Input: events= [[1,2],[2,3],[3,4],[1,2]]
Output: 4
 

Constraints:

1 <= events.length <= 105
events[i].length == 2
1 <= startDayi <= endDayi <= 105

# Code
```cpp []
class Solution {
public:
    int maxEvents(vector<vector<int>>& events) {
        int ans = 0;
        int d = 0; // the current day
        int i = 0; // events' index
        priority_queue<int, vector<int>, greater<>> minHeap;

        ranges::sort(events);

        while (!minHeap.empty() || i < events.size()) {
            // If no events are available to attend today, let time flies to the
            // next available event.
            if (minHeap.empty())
                d = events[i][0];
            // All the events starting from today are newly available.
            while (i < events.size() && events[i][0] == d)
                minHeap.push(events[i++][1]);
            // Greedily attend the event that'll end the earliest since it has
            // higher chance can't be attended in the future.
            minHeap.pop();
            ++ans;
            ++d;
            // Pop the events that can't be attended.
            while (!minHeap.empty() && minHeap.top() < d)
                minHeap.pop();
        }

        return ans;
    }
};
```

-------



# 203. Remove Linked List Elements -> [LeetCode](https://leetcode.com/problems/remove-linked-list-elements/description/)
Easy

Given the head of a linked list and an integer val, remove all the nodes of the linked list that has Node.val == val, and return the new head.

 

Example 1:


Input: head = [1,2,6,3,4,5,6], val = 6
Output: [1,2,3,4,5]


Example 2:

Input: head = [], val = 1
Output: []


Example 3:

Input: head = [7,7,7,7], val = 7
Output: []
 

Constraints:

The number of nodes in the list is in the range [0, 104].
1 <= Node.val <= 50
0 <= val <= 50

# Code
```cpp []
class Solution {
 public:
  ListNode* removeElements(ListNode* head, int val) {
    ListNode dummy(0, head);
    ListNode* prev = &dummy;

    for (; head; head = head->next)
      if (head->val != val) {
        prev->next = head;
        prev = prev->next;
      }
    prev->next = nullptr;  // In case that the last value equals `val`.

    return dummy.next;
  }
};
```

-------



# 1751. Maximum Number of Events That Can Be Attended II -> [LeetCode](https://leetcode.com/problems/maximum-number-of-events-that-can-be-attended-ii/description)

Hard

You are given an array of events where events[i] = [startDayi, endDayi, valuei]. The ith event starts at startDayi and ends at endDayi, and if you attend this event, you will receive a value of valuei. You are also given an integer k which represents the maximum number of events you can attend.

You can only attend one event at a time. If you choose to attend an event, you must attend the entire event. Note that the end day is inclusive: that is, you cannot attend two events where one of them starts and the other ends on the same day.

Return the maximum sum of values that you can receive by attending events.

 

Example 1:



Input: events = [[1,2,4],[3,4,3],[2,3,1]], k = 2
Output: 7
Explanation: Choose the green events, 0 and 1 (0-indexed) for a total value of 4 + 3 = 7.


Example 2:



Input: events = [[1,2,4],[3,4,3],[2,3,10]], k = 2
Output: 10
Explanation: Choose event 2 for a total value of 10.
Notice that you cannot attend any other event as they overlap, and that you do not have to attend k events.


Example 3:



Input: events = [[1,1,1],[2,2,2],[3,3,3],[4,4,4]], k = 3
Output: 9
Explanation: Although the events do not overlap, you can only attend 3 events. Pick the highest valued three.
 

Constraints:

1 <= k <= events.length
1 <= k * events.length <= 106
1 <= startDayi <= endDayi <= 109
1 <= valuei <= 106

# Code
```cpp []
class Solution {
public:
    int maxValue(vector<vector<int>>& events, int k) {
        vector<vector<int>> mem(events.size(), vector<int>(k + 1, -1));
        ranges::sort(events);
        return maxValue(events, 0, k, mem);
    }

private:
    // Returns the maximum sum of values that you can receive by attending
    // events[i..n), where k is the maximum number of attendancevents.
    int maxValue(const vector<vector<int>>& events, int i, int k,
                 vector<vector<int>>& mem) {
        if (k == 0 || i == events.size())
            return 0;
        if (mem[i][k] != -1)
            return mem[i][k];

        // Binary search `events` to find the first index j
        // s.t. events[j][0] > events[i][1].
        const auto it = upper_bound(
            events.begin() + i, events.end(), events[i][1],
            [](int end, const vector<int>& event) { return event[0] > end; });
        const int j = distance(events.begin(), it);
        return mem[i][k] = max(events[i][2] + maxValue(events, j, k - 1, mem),
                               maxValue(events, i + 1, k, mem));
    }
};
```

------


# 735. Asteroid Collision -> [LeetCode](https://leetcode.com/problems/asteroid-collision/description/)

Medium

We are given an array asteroids of integers representing asteroids in a row. The indices of the asteriod in the array represent their relative position in space.

For each asteroid, the absolute value represents its size, and the sign represents its direction (positive meaning right, negative meaning left). Each asteroid moves at the same speed.

Find out the state of the asteroids after all collisions. If two asteroids meet, the smaller one will explode. If both are the same size, both will explode. Two asteroids moving in the same direction will never meet.

 

Example 1:

Input: asteroids = [5,10,-5]
Output: [5,10]
Explanation: The 10 and -5 collide resulting in 10. The 5 and 10 never collide.


Example 2:

Input: asteroids = [8,-8]
Output: []
Explanation: The 8 and -8 collide exploding each other.


Example 3:

Input: asteroids = [10,2,-5]
Output: [10]
Explanation: The 2 and -5 collide resulting in -5. The 10 and -5 collide resulting in 10.
 

Constraints:

2 <= asteroids.length <= 104
-1000 <= asteroids[i] <= 1000
asteroids[i] != 0

# Code
```cpp []
class Solution {
public:
    vector<int> asteroidCollision(vector<int>& nums) {
        vector<int> ans;

        for(const int n:nums){
            bool isExplode = false;
            while(!ans.empty() && n < 0 && ans.back() > 0){
                if(abs(ans.back()) < abs(n)) ans.pop_back();
                else if(abs(ans.back()) == abs(n)){
                    ans.pop_back();
                    isExplode = true;
                    break;
                }else{
                    isExplode = true;
                    break;
                }
            }

            if(!isExplode) ans.push_back(n);
        }

        return ans;
    }
};
```

---------


# 150. Evaluate Reverse Polish Notation -> [LeetCode](https://leetcode.com/problems/evaluate-reverse-polish-notation/description/)

Medium

You are given an array of strings tokens that represents an arithmetic expression in a Reverse Polish Notation.

Evaluate the expression. Return an integer that represents the value of the expression.

Note that:

The valid operators are '+', '-', '*', and '/'.
Each operand may be an integer or another expression.
The division between two integers always truncates toward zero.
There will not be any division by zero.
The input represents a valid arithmetic expression in a reverse polish notation.
The answer and all the intermediate calculations can be represented in a 32-bit integer.
 

Example 1:

Input: tokens = ["2","1","+","3","*"]
Output: 9
Explanation: ((2 + 1) * 3) = 9


Example 2:

Input: tokens = ["4","13","5","/","+"]
Output: 6
Explanation: (4 + (13 / 5)) = 6


Example 3:

Input: tokens = ["10","6","9","3","+","-11","*","/","*","17","+","5","+"]
Output: 22
Explanation: ((10 * (6 / ((9 + 3) * -11))) + 17) + 5
= ((10 * (6 / (12 * -11))) + 17) + 5
= ((10 * (6 / -132)) + 17) + 5
= ((10 * 0) + 17) + 5
= (0 + 17) + 5
= 17 + 5
= 22
 

Constraints:

1 <= tokens.length <= 104
tokens[i] is either an operator: "+", "-", "*", or "/", or an integer in the range [-200, 200].

# Code
```cpp []
class Solution {
public:
    int evalRPN(vector<string>& tokens) {
        stack<int> ans;

        for (const string& s : tokens) {
            if (s == "+" || s == "-" || s == "*" || s == "/") {
                int y = ans.top();
                ans.pop();
                int x = ans.top();
                ans.pop();

                if (s == "+") {
                    ans.push((x + y));
                    continue;
                }
                if (s == "-") {
                    ans.push((x - y));
                    continue;
                }
                if (s == "*") {
                    ans.push((x * y));
                    continue;
                }
                if (s == "/") {
                    ans.push((x / y));
                    continue;
                }

            } else {
                ans.push(stoi(s));
            }
        }

        return ans.top();
    }
};
```

-------



# 3439. Reschedule Meetings for Maximum Free Time I -> [LeetCode](https://leetcode.com/problems/reschedule-meetings-for-maximum-free-time-i/description/)

Medium

You are given an integer eventTime denoting the duration of an event, where the event occurs from time t = 0 to time t = eventTime.

You are also given two integer arrays startTime and endTime, each of length n. These represent the start and end time of n non-overlapping meetings, where the ith meeting occurs during the time [startTime[i], endTime[i]].

You can reschedule at most k meetings by moving their start time while maintaining the same duration, to maximize the longest continuous period of free time during the event.

The relative order of all the meetings should stay the same and they should remain non-overlapping.

Return the maximum amount of free time possible after rearranging the meetings.

Note that the meetings can not be rescheduled to a time outside the event.

 

Example 1:

Input: eventTime = 5, k = 1, startTime = [1,3], endTime = [2,5]

Output: 2

Explanation:



Reschedule the meeting at [1, 2] to [2, 3], leaving no meetings during the time [0, 2].

Example 2:

Input: eventTime = 10, k = 1, startTime = [0,2,9], endTime = [1,4,10]

Output: 6

Explanation:



Reschedule the meeting at [2, 4] to [1, 3], leaving no meetings during the time [3, 9].

Example 3:

Input: eventTime = 5, k = 2, startTime = [0,1,2,3,4], endTime = [1,2,3,4,5]

Output: 0

Explanation:

There is no time during the event not occupied by meetings.

 

Constraints:

1 <= eventTime <= 109
n == startTime.length == endTime.length
2 <= n <= 105
1 <= k <= n
0 <= startTime[i] < endTime[i] <= eventTime
endTime[i] <= startTime[i + 1] where i lies in the range [0, n - 2].


# Code
```cpp []
class Solution {
public:
    int maxFreeTime(int eventTime, int k, vector<int>& startTime,
                    vector<int>& endTime) {
        const vector<int> gaps = getGaps(eventTime, startTime, endTime);
        int windowSum = accumulate(gaps.begin(), gaps.begin() + k + 1, 0);
        int ans = windowSum;

        for (int i = k + 1; i < gaps.size(); ++i) {
            windowSum += gaps[i] - gaps[i - k - 1];
            ans = max(ans, windowSum);
        }

        return ans;
    }

private:
    vector<int> getGaps(int eventTime, const vector<int>& startTime,
                        const vector<int>& endTime) {
        vector<int> gaps{startTime[0]};
        for (int i = 1; i < startTime.size(); ++i)
            gaps.push_back(startTime[i] - endTime[i - 1]);
        gaps.push_back(eventTime - endTime.back());
        return gaps;
    }
};
```

------




# 3440. Reschedule Meetings for Maximum Free Time II -> [LeetCode](https://leetcode.com/problems/reschedule-meetings-for-maximum-free-time-ii/description)

Medium

You are given an integer eventTime denoting the duration of an event. You are also given two integer arrays startTime and endTime, each of length n.

These represent the start and end times of n non-overlapping meetings that occur during the event between time t = 0 and time t = eventTime, where the ith meeting occurs during the time [startTime[i], endTime[i]].

You can reschedule at most one meeting by moving its start time while maintaining the same duration, such that the meetings remain non-overlapping, to maximize the longest continuous period of free time during the event.

Return the maximum amount of free time possible after rearranging the meetings.

Note that the meetings can not be rescheduled to a time outside the event and they should remain non-overlapping.

Note: In this version, it is valid for the relative ordering of the meetings to change after rescheduling one meeting.

 

Example 1:

Input: eventTime = 5, startTime = [1,3], endTime = [2,5]

Output: 2

Explanation:



Reschedule the meeting at [1, 2] to [2, 3], leaving no meetings during the time [0, 2].

Example 2:

Input: eventTime = 10, startTime = [0,7,9], endTime = [1,8,10]

Output: 7

Explanation:



Reschedule the meeting at [0, 1] to [8, 9], leaving no meetings during the time [0, 7].

Example 3:

Input: eventTime = 10, startTime = [0,3,7,9], endTime = [1,4,8,10]

Output: 6

Explanation:



Reschedule the meeting at [3, 4] to [8, 9], leaving no meetings during the time [1, 7].

Example 4:

Input: eventTime = 5, startTime = [0,1,2,3,4], endTime = [1,2,3,4,5]

Output: 0

Explanation:

There is no time during the event not occupied by meetings.

 

Constraints:

1 <= eventTime <= 109
n == startTime.length == endTime.length
2 <= n <= 105
0 <= startTime[i] < endTime[i] <= eventTime
endTime[i] <= startTime[i + 1] where i lies in the range [0, n - 2].

# Code
```cpp []
class Solution {
public:
    int maxFreeTime(int eventTime, vector<int>& startTime,
                    vector<int>& endTime) {
        const int n = startTime.size();
        const vector<int> gaps = getGaps(eventTime, startTime, endTime);
        int ans = 0;
        vector<int> maxLeft(n + 1);  
        vector<int> maxRight(n + 1); 

        maxLeft[0] = gaps[0];
        maxRight[n] = gaps[n];

        for (int i = 1; i < n + 1; ++i)
            maxLeft[i] = max(gaps[i], maxLeft[i - 1]);

        for (int i = n - 1; i >= 0; --i)
            maxRight[i] = max(gaps[i], maxRight[i + 1]);

        for (int i = 0; i < n; ++i) {
            const int currMeetingTime = endTime[i] - startTime[i];
            const int adjacentGapsSum = gaps[i] + gaps[i + 1];
            const bool canMoveMeeting =
                currMeetingTime <= max(i > 0 ? maxLeft[i - 1] : 0, //
                                       i + 2 < n + 1 ? maxRight[i + 2] : 0);
            ans = max(ans,
                      adjacentGapsSum + (canMoveMeeting ? currMeetingTime : 0));
        }

        return ans;
    }

private:
    vector<int> getGaps(int eventTime, const vector<int>& startTime,
                        const vector<int>& endTime) {
        vector<int> gaps{startTime[0]};
        for (int i = 1; i < startTime.size(); ++i)
            gaps.push_back(startTime[i] - endTime[i - 1]);
        gaps.push_back(eventTime - endTime.back());
        return gaps;
    }
};
```

-------

# 692. Top K Frequent Words -> [LeetCode](https://leetcode.com/problems/top-k-frequent-words/description/)

Medium

Given an array of strings words and an integer k, return the k most frequent strings.

Return the answer sorted by the frequency from highest to lowest. Sort the words with the same frequency by their lexicographical order.

 

Example 1:

Input: words = ["i","love","leetcode","i","love","coding"], k = 2
Output: ["i","love"]
Explanation: "i" and "love" are the two most frequent words.
Note that "i" comes before "love" due to a lower alphabetical order.

Example 2:

Input: words = ["the","day","is","sunny","the","the","the","sunny","is","is"], k = 4
Output: ["the","is","sunny","day"]
Explanation: "the", "is", "sunny" and "day" are the four most frequent words, with the number of occurrence being 4, 3, 2 and 1 respectively.
 

Constraints:

1 <= words.length <= 500
1 <= words[i].length <= 10
words[i] consists of lowercase English letters.
k is in the range [1, The number of unique words[i]]
 

Follow-up: Could you solve it in O(n log(k)) time and O(n) extra space?

# Code
```cpp []
class Solution {
public:
    vector<string> topKFrequent(vector<string>& words, int k) {

        map<string, int> freq;

        for (auto i : words) {
            freq[i]++;
        }

        vector<string> ans;

        vector<pair<string, int>> pp(freq.begin(), freq.end());

        sort(pp.begin(), pp.end(),
             [](pair<string, int>& a, pair<string, int>& b) {
                if(a.second == b.second){
                    return a.first < b.first;
                }
                 return a.second > b.second;
             });

        int count = 0;

        for (auto it : pp) {
            if (count == k)
                break;
            // cout << it.first << " : " << it.second << endl;
            ans.push_back(it.first);
            count++;
        }

        return ans;
    }
};
```

-------


# 2402. Meeting Rooms III -> [Leetcode](https://leetcode.com/problems/meeting-rooms-iii/description/)

Hard

You are given an integer n. There are n rooms numbered from 0 to n - 1.

You are given a 2D integer array meetings where meetings[i] = [starti, endi] means that a meeting will be held during the half-closed time interval [starti, endi). All the values of starti are unique.

Meetings are allocated to rooms in the following manner:

Each meeting will take place in the unused room with the lowest number.
If there are no available rooms, the meeting will be delayed until a room becomes free. The delayed meeting should have the same duration as the original meeting.
When a room becomes unused, meetings that have an earlier original start time should be given the room.
Return the number of the room that held the most meetings. If there are multiple rooms, return the room with the lowest number.

A half-closed interval [a, b) is the interval between a and b including a and not including b.

 

Example 1:

Input: n = 2, meetings = [[0,10],[1,5],[2,7],[3,4]]
Output: 0
Explanation:
- At time 0, both rooms are not being used. The first meeting starts in room 0.
- At time 1, only room 1 is not being used. The second meeting starts in room 1.
- At time 2, both rooms are being used. The third meeting is delayed.
- At time 3, both rooms are being used. The fourth meeting is delayed.
- At time 5, the meeting in room 1 finishes. The third meeting starts in room 1 for the time period [5,10).
- At time 10, the meetings in both rooms finish. The fourth meeting starts in room 0 for the time period [10,11).
Both rooms 0 and 1 held 2 meetings, so we return 0. 


Example 2:

Input: n = 3, meetings = [[1,20],[2,10],[3,5],[4,9],[6,8]]
Output: 1
Explanation:
- At time 1, all three rooms are not being used. The first meeting starts in room 0.
- At time 2, rooms 1 and 2 are not being used. The second meeting starts in room 1.
- At time 3, only room 2 is not being used. The third meeting starts in room 2.
- At time 4, all three rooms are being used. The fourth meeting is delayed.
- At time 5, the meeting in room 2 finishes. The fourth meeting starts in room 2 for the time period [5,10).
- At time 6, all three rooms are being used. The fifth meeting is delayed.
- At time 10, the meetings in rooms 1 and 2 finish. The fifth meeting starts in room 1 for the time period [10,12).
Room 0 held 1 meeting while rooms 1 and 2 each held 2 meetings, so we return 1. 
 

Constraints:

1 <= n <= 100
1 <= meetings.length <= 105
meetings[i].length == 2
0 <= starti < endi <= 5 * 105
All the values of starti are unique.

# Code
```cpp []
struct T {
    long endTime;
    int roomId;
};

class Solution {
public:
    int mostBooked(int n, vector<vector<int>>& meetings) {
        vector<int> count(n);

        ranges::sort(meetings);

        auto compare = [](const T& a, const T& b) {
            return a.endTime == b.endTime ? a.roomId > b.roomId
                                          : a.endTime > b.endTime;
        };
        priority_queue<T, vector<T>, decltype(compare)> occupied(compare);
        priority_queue<int, vector<int>, greater<>> availableRoomIds;

        for (int i = 0; i < n; ++i)
            availableRoomIds.push(i);

        for (const vector<int>& meeting : meetings) {
            const int start = meeting[0];
            const int end = meeting[1];
            // Push meetings ending before this `meeting` in occupied to the
            // `availableRoomsIds`.
            while (!occupied.empty() && occupied.top().endTime <= start)
                availableRoomIds.push(occupied.top().roomId), occupied.pop();
            if (availableRoomIds.empty()) {
                const auto [newStart, roomId] = occupied.top();
                occupied.pop();
                ++count[roomId];
                occupied.push({newStart + (end - start), roomId});
            } else {
                const int roomId = availableRoomIds.top();
                availableRoomIds.pop();
                ++count[roomId];
                occupied.push({end, roomId});
            }
        }

        return ranges::max_element(count) - count.begin();
    }
};
```

------


# 706. Design HashMap -> [Leetcode](https://leetcode.com/problems/design-hashmap/description/)

Easy

Design a HashMap without using any built-in hash table libraries.

Implement the MyHashMap class:

MyHashMap() initializes the object with an empty map.
void put(int key, int value) inserts a (key, value) pair into the HashMap. If the key already exists in the map, update the corresponding value.
int get(int key) returns the value to which the specified key is mapped, or -1 if this map contains no mapping for the key.
void remove(key) removes the key and its corresponding value if the map contains the mapping for the key.
 

Example 1:

Input
["MyHashMap", "put", "put", "get", "get", "put", "get", "remove", "get"]
[[], [1, 1], [2, 2], [1], [3], [2, 1], [2], [2], [2]]
Output
[null, null, null, 1, -1, null, 1, null, -1]

Explanation
MyHashMap myHashMap = new MyHashMap();
myHashMap.put(1, 1); // The map is now [[1,1]]
myHashMap.put(2, 2); // The map is now [[1,1], [2,2]]
myHashMap.get(1);    // return 1, The map is now [[1,1], [2,2]]
myHashMap.get(3);    // return -1 (i.e., not found), The map is now [[1,1], [2,2]]
myHashMap.put(2, 1); // The map is now [[1,1], [2,1]] (i.e., update the existing value)
myHashMap.get(2);    // return 1, The map is now [[1,1], [2,1]]
myHashMap.remove(2); // remove the mapping for 2, The map is now [[1,1]]
myHashMap.get(2);    // return -1 (i.e., not found), The map is now [[1,1]]
 

Constraints:

0 <= key, value <= 106
At most 104 calls will be made to put, get, and remove.

# Code
```cpp []
class MyHashMap {
    static const int SIZE = 1000001;
    int mp[SIZE];

public:
    MyHashMap() {
        fill(mp,mp + SIZE , -1);
    }

    void put(int key, int value) { mp[key] = value; }

    int get(int key) {
        return (mp[key]);
    }

    void remove(int key) { mp[key] = -1; }
};

/**
 * Your MyHashMap object will be instantiated and called as such:
 * MyHashMap* obj = new MyHashMap();
 * obj->put(key,value);
 * int param_2 = obj->get(key);
 * obj->remove(key);
 */
```

----



# 144. Binary Tree Preorder Traversal -> [LeetCode](https://leetcode.com/problems/binary-tree-preorder-traversal/description/)

Easy

Given the root of a binary tree, return the preorder traversal of its nodes' values.

 

Example 1:

Input: root = [1,null,2,3]

Output: [1,2,3]

Explanation:



Example 2:

Input: root = [1,2,3,4,5,null,8,null,null,6,7,9]

Output: [1,2,4,5,6,7,3,8,9]

Explanation:



Example 3:

Input: root = []

Output: []

Example 4:

Input: root = [1]

Output: [1]

 

Constraints:

The number of nodes in the tree is in the range [0, 100].
-100 <= Node.val <= 100
 

# Code
```cpp []
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
private:
    void preOrder(TreeNode* root , vector<int> &ans){
        if(root == nullptr) return;
        ans.push_back(root->val);
        preOrder(root->left , ans);        
        preOrder(root->right , ans);        
    }
public:
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> ans;

        preOrder(root , ans);

        return ans;
    }
};
```

-----


# 958. Check Completeness of a Binary Tree -> [LeetCode](https://leetcode.com/problems/check-completeness-of-a-binary-tree/description/)

Medium

Given the root of a binary tree, determine if it is a complete binary tree.

In a complete binary tree, every level, except possibly the last, is completely filled, and all nodes in the last level are as far left as possible. It can have between 1 and 2h nodes inclusive at the last level h.

 

Example 1:


Input: root = [1,2,3,4,5,6]
Output: true
Explanation: Every level before the last is full (ie. levels with node-values {1} and {2, 3}), and all nodes in the last level ({4, 5, 6}) are as far left as possible.


Example 2:


Input: root = [1,2,3,4,5,null,7]
Output: false
Explanation: The node with value 7 isn't as far left as possible.
 

Constraints:

The number of nodes in the tree is in the range [1, 100].
1 <= Node.val <= 1000

# Code
```cpp []
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    bool isCompleteTree(TreeNode* root) {
        if(root == nullptr) return true;

        queue<TreeNode*> q;
        q.push(root);

        while(q.front() != nullptr){
            TreeNode* cur = q.front(); q.pop();
            q.push(cur->left);
            q.push(cur->right);
        }

        while(q.front() == nullptr){
            q.pop();
        }

        return q.empty();

    }
};
```

-----


# 622. Design Circular Queue -> [LeetCode](https://leetcode.com/problems/design-circular-queue/description/)

Medium

Design your implementation of the circular queue. The circular queue is a linear data structure in which the operations are performed based on FIFO (First In First Out) principle, and the last position is connected back to the first position to make a circle. It is also called "Ring Buffer".

One of the benefits of the circular queue is that we can make use of the spaces in front of the queue. In a normal queue, once the queue becomes full, we cannot insert the next element even if there is a space in front of the queue. But using the circular queue, we can use the space to store new values.

Implement the MyCircularQueue class:

MyCircularQueue(k) Initializes the object with the size of the queue to be k.
int Front() Gets the front item from the queue. If the queue is empty, return -1.
int Rear() Gets the last item from the queue. If the queue is empty, return -1.
boolean enQueue(int value) Inserts an element into the circular queue. Return true if the operation is successful.
boolean deQueue() Deletes an element from the circular queue. Return true if the operation is successful.
boolean isEmpty() Checks whether the circular queue is empty or not.
boolean isFull() Checks whether the circular queue is full or not.
You must solve the problem without using the built-in queue data structure in your programming language. 

 

Example 1:

Input
["MyCircularQueue", "enQueue", "enQueue", "enQueue", "enQueue", "Rear", "isFull", "deQueue", "enQueue", "Rear"]
[[3], [1], [2], [3], [4], [], [], [], [4], []]
Output
[null, true, true, true, false, 3, true, true, true, 4]

Explanation
MyCircularQueue myCircularQueue = new MyCircularQueue(3);
myCircularQueue.enQueue(1); // return True
myCircularQueue.enQueue(2); // return True
myCircularQueue.enQueue(3); // return True
myCircularQueue.enQueue(4); // return False
myCircularQueue.Rear();     // return 3
myCircularQueue.isFull();   // return True
myCircularQueue.deQueue();  // return True
myCircularQueue.enQueue(4); // return True
myCircularQueue.Rear();     // return 4
 

Constraints:

1 <= k <= 1000
0 <= value <= 1000
At most 3000 calls will be made to enQueue, deQueue, Front, Rear, isEmpty, and isFull.

# Code
```cpp []
class MyCircularQueue {
    int size;
    int *arr;
    int front;
    int rear;
    int count;
public:
    MyCircularQueue(int k) {
        size = k;
        arr = new int[size];
        front = -1;
        rear = -1;
        count = 0;
    }
    
    bool enQueue(int value) {
        if(isFull()) return false;
        if(front == -1) front = 0;
        rear = (rear + 1) % size;
        arr[rear] = value;
        count++;
        return true;
    }
    
    bool deQueue() {
        if(isEmpty()) return false;
        front = (front + 1) % size;
        count--;
        return true;
    }
    
    int Front() {
        return isEmpty() ? -1 : arr[front];
    }
    
    int Rear() {
        return isEmpty() ? -1 : arr[rear];
    }
    
    bool isEmpty() {
        if(count == 0) return true;
        return false;
    }
    
    bool isFull() {
        if(count == size) return true;
        return false;
    }
};

/**
 * Your MyCircularQueue object will be instantiated and called as such:
 * MyCircularQueue* obj = new MyCircularQueue(k);
 * bool param_1 = obj->enQueue(value);
 * bool param_2 = obj->deQueue();
 * int param_3 = obj->Front();
 * int param_4 = obj->Rear();
 * bool param_5 = obj->isEmpty();
 * bool param_6 = obj->isFull();
 */
```

------

# 1342. Number of Steps to Reduce a Number to Zero -> [LeetCode](https://leetcode.com/problems/number-of-steps-to-reduce-a-number-to-zero/description/)
Easy

Given an integer num, return the number of steps to reduce it to zero.

In one step, if the current number is even, you have to divide it by 2, otherwise, you have to subtract 1 from it.

 

Example 1:

Input: num = 14
Output: 6
Explanation: 
Step 1) 14 is even; divide by 2 and obtain 7. 
Step 2) 7 is odd; subtract 1 and obtain 6.
Step 3) 6 is even; divide by 2 and obtain 3. 
Step 4) 3 is odd; subtract 1 and obtain 2. 
Step 5) 2 is even; divide by 2 and obtain 1. 
Step 6) 1 is odd; subtract 1 and obtain 0.


Example 2:

Input: num = 8
Output: 4
Explanation: 
Step 1) 8 is even; divide by 2 and obtain 4. 
Step 2) 4 is even; divide by 2 and obtain 2. 
Step 3) 2 is even; divide by 2 and obtain 1. 
Step 4) 1 is odd; subtract 1 and obtain 0.


Example 3:

Input: num = 123
Output: 12
 

Constraints:

0 <= num <= 106

# Code
```cpp []
class Solution {
public:
    int numberOfSteps(int num) {
        int ans = 0;

        while(num){
            if(num % 2 == 0){
                num /= 2;
                ans++;
                continue;
            }
            num--;
            ans++;
        }

        return ans;
    }
};
```

------

# 1900. The Earliest and Latest Rounds Where Players Compete -> [LeetCode](https://leetcode.com/problems/the-earliest-and-latest-rounds-where-players-compete/description/)

Hard

There is a tournament where n players are participating. The players are standing in a single row and are numbered from 1 to n based on their initial standing position (player 1 is the first player in the row, player 2 is the second player in the row, etc.).

The tournament consists of multiple rounds (starting from round number 1). In each round, the ith player from the front of the row competes against the ith player from the end of the row, and the winner advances to the next round. When the number of players is odd for the current round, the player in the middle automatically advances to the next round.

For example, if the row consists of players 1, 2, 4, 6, 7
Player 1 competes against player 7.
Player 2 competes against player 6.
Player 4 automatically advances to the next round.
After each round is over, the winners are lined back up in the row based on the original ordering assigned to them initially (ascending order).

The players numbered firstPlayer and secondPlayer are the best in the tournament. They can win against any other player before they compete against each other. If any two other players compete against each other, either of them might win, and thus you may choose the outcome of this round.

Given the integers n, firstPlayer, and secondPlayer, return an integer array containing two values, the earliest possible round number and the latest possible round number in which these two players will compete against each other, respectively.

 

Example 1:

Input: n = 11, firstPlayer = 2, secondPlayer = 4
Output: [3,4]
Explanation:
One possible scenario which leads to the earliest round number:
First round: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11
Second round: 2, 3, 4, 5, 6, 11
Third round: 2, 3, 4
One possible scenario which leads to the latest round number:
First round: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11
Second round: 1, 2, 3, 4, 5, 6
Third round: 1, 2, 4
Fourth round: 2, 4

Example 2:

Input: n = 5, firstPlayer = 1, secondPlayer = 5
Output: [1,1]
Explanation: The players numbered 1 and 5 compete in the first round.
There is no way to make them compete in any other round.
 

Constraints:

2 <= n <= 28
1 <= firstPlayer < secondPlayer <= n

# Code
```cpp []
class Solution {
 public:
  vector<int> earliestAndLatest(int n, int firstPlayer, int secondPlayer) {
    using P = pair<int, int>;
    vector<vector<vector<P>>> mem(n + 1,
                                  vector<vector<P>>(n + 1, vector<P>(n + 1)));
    const auto [a, b] = solve(firstPlayer, n - secondPlayer + 1, n, mem);
    return {a, b};
  }

 private:
  // Returns the (earliest, latest) pair, the first player is the l-th player
  // from the front, the second player is the r-th player from the end, and
  // there're k people.
  pair<int, int> solve(int l, int r, int k,
                       vector<vector<vector<pair<int, int>>>>& mem) {
    if (l == r)
      return {1, 1};
    if (l > r)
      swap(l, r);
    if (mem[l][r][k] != pair<int, int>{0, 0})
      return mem[l][r][k];

    int a = INT_MAX;
    int b = INT_MIN;

    // Enumerate all the possible positions.
    for (int i = 1; i <= l; ++i)
      for (int j = l - i + 1; j <= r - i; ++j) {
        if (i + j > (k + 1) / 2 || i + j < l + r - k / 2)
          continue;
        const auto [x, y] = solve(i, j, (k + 1) / 2, mem);
        a = min(a, x + 1);
        b = max(b, y + 1);
      }

    return mem[l][r][k] = {a, b};
  }
};
```

-----




