
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


