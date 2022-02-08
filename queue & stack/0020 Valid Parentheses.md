# 20. Valid Parentheses
https://leetcode-cn.com/problems/valid-parentheses  
Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.  

An input string is valid if:  
Open brackets must be closed by the same type of brackets.  
Open brackets must be closed in the correct order.  
 
Example 1:  
Input: s = "()"  
Output: true  

Example 2:  
Input: s = "()[]{}"  
Output: true  

Example 3:  
Input: s = "(]"  
Output: false  

Constraints:  
1 <= s.length <= 104  
s consists of parentheses only '()[]{}'.  

``` cpp
class Solution {
public:
    bool isValid(string s) {
        int n = s.size();
        if (n % 2 == 1) {
            return false;
        }

        unordered_map<char, char> pairs = {
            {')', '('},
            {']', '['},
            {'}', '{'}
        };
        stack<char> stk;
        for (char ch: s) {
            if (pairs.count(ch)) {
                if (stk.empty() || stk.top() != pairs[ch]) {
                    return false;
                }
                stk.pop();
            }
            else {
                stk.push(ch);
            }
        }
        return stk.empty();
    }
};
```
