# 32. Longest Valid Parentheses
https://leetcode-cn.com/problems/longest-valid-parentheses  
Given a string containing just the characters '(' and ')', find the length of the longest valid (well-formed) parentheses substring.  

Example 1:  
Input: s = "(()"  
Output: 2  
Explanation: The longest valid parentheses substring is "()".  

Example 2:  
Input: s = ")()())"  
Output: 4  
Explanation: The longest valid parentheses substring is "()()".  

Example 3:  
Input: s = ""  
Output: 0  

Constraints:
0 <= s.length <= 3 * 10^4  
s[i] is '(', or ')'.  

``` cpp
class Solution {
public:
    int longestValidParentheses(string s) {
        int left=0,right=0,ans=0,tmp=0;
        stack<int> stk;
        stk.push(-1);
        for(int i=0;i<s.size();i++){
            if (s[i]=='(') stk.push(i);
            else{
                stk.pop();
                if (stk.empty()){
                    stk.push(i);
                } else {
                    ans=max(ans,i-stk.top());
                }
            }
        }
        
        return ans;
    }
};
```
