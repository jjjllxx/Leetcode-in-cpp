# 10. Regular Expression Matching
https://leetcode-cn.com/problems/regular-expression-matching  
Given an input string s and a pattern p, implement regular expression matching with support for '.' and '*' where:  
'.' Matches any single character.  
'*' Matches zero or more of the preceding element.  
The matching should cover the entire input string (not partial).  

Example 1:  
Input: s = "aa", p = "a"  
Output: false  
Explanation: "a" does not match the entire string "aa".  

Example 2:  
Input: s = "aa", p = "a*"  
Output: true  
Explanation: '*' means zero or more of the preceding element, 'a'. Therefore, by repeating 'a' once, it becomes "aa".  

Example 3:  
Input: s = "ab", p = ".*"  
Output: true  
Explanation: ".*" means "zero or more (*) of any character (.)".  

Constraints:  
1 <= s.length <= 20  
1 <= p.length <= 30  
s contains only lowercase English letters.  
p contains only lowercase English letters, '.', and '*'.  
It is guaranteed for each appearance of the character '*', there will be a previous valid character to match.  

``` cpp
class Solution {
public:
    bool isMatch(string s, string p) {
        int n=s.size(),m=p.size();
        vector<vector<int>> dp(m+1,vector<int>(n+1,0));
        dp[0][0]=1;
        for(int i=1;i<=m;i++){
            if (i>=2 && p[i-1]=='*') dp[i][0]=dp[i-2][0];
            for(int j=1;j<=n;j++){
                if(p[i-1]=='.' || p[i-1]==s[j-1]) {
                    dp[i][j]=dp[i-1][j-1];
                }
                else {
                    if (p[i-1]=='*'&& i>=2) {
                        if (p[i-2]==s[j-1]||p[i-2]=='.') {
                            dp[i][j]=(dp[i][j-1]|dp[i-2][j]);
                        }
                        else {
                            dp[i][j]=dp[i-2][j];
                        }
                    }
                }
            }
        }
        return dp[m][n];
    }
};
```
