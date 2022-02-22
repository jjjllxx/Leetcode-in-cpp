# 139. Word Break
https://leetcode-cn.com/problems/word-break/  
Given a string s and a dictionary of strings wordDict, return true if s can be segmented into a space-separated sequence of one or more dictionary words.  
Note that the same word in the dictionary may be reused multiple times in the segmentation.  

Example 1:  
Input: s = "leetcode", wordDict = ["leet","code"]  
Output: true  
Explanation: Return true because "leetcode" can be segmented as "leet code".  

Example 2:   
Input: s = "applepenapple", wordDict = ["apple","pen"]  
Output: true   
Explanation: Return true because "applepenapple" can be segmented as "apple pen apple".  
Note that you are allowed to reuse a dictionary word.  

Example 3:  
Input: s = "catsandog", wordDict = ["cats","dog","sand","and","cat"]  
Output: false  

Constraints:  
1 <= s.length <= 300  
1 <= wordDict.length <= 1000  
1 <= wordDict[i].length <= 20  
s and wordDict[i] consist of only lowercase English letters.  
All the strings of wordDict are unique.  

``` cpp
class Solution {
public:
    bool wordBreak(string s, vector<string>& wordDict) {
        int n=s.size(),left=n, right=0;
        vector<bool> dp(n+1,false);
        dp[0]=true;
        unordered_map<int,vector<string>> mp;
        for (string word:wordDict) {
            int m=word.length();
            right=max({right, m});
            left=min({left, m});
            mp[m].emplace_back(word);
        }
        for(int i=0; i<=n; i++){
            if (dp[i]){
                for(int j=left; j<=min({right,n-i}); j++){
                    for (string x:mp[j]){
                        if (s.substr(i,j)==x){
                            dp[i+j]=true;
                            break;
                        }
                    }
                }
            }
        }
        return dp[n];
    }
};
```
