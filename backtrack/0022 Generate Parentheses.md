# 22. Generate Parentheses
https://leetcode-cn.com/problems/generate-parentheses  
Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.  

Example 1:  
Input: n = 3  
Output: ["((()))","(()())","(())()","()(())","()()()"]  

Example 2:  
Input: n = 1  
Output: ["()"]  

Constraints:  
1 <= n <= 8 

``` cpp
class Solution {
    void backtrack(vector<string>& res,string s,int left,int right,int n){
            if (s.size()==n*2){
                res.push_back(s);
                return;
            }
            if (left<n){
                s.push_back('(');
                backtrack(res,s,left+1,right,n);
                s.pop_back();
            }
            if (right<left){
                s.push_back(')');
                backtrack(res,s,left,right+1,n);
                s.pop_back();
            }
        }
public:
    vector<string> generateParenthesis(int n) {
        vector<string> ans;
        backtrack(ans,"",0,0,n);
        return ans;
    }
};
```
