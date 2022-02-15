# 72. Edit Distance
https://leetcode-cn.com/problems/edit-distance  
Given two strings word1 and word2, return the minimum number of operations required to convert word1 to word2.  
You have the following three operations permitted on a word:  
Insert a character  
Delete a character  
Replace a character  

Example 1:  
Input: word1 = "horse", word2 = "ros"  
Output: 3  
Explanation:   
horse -> rorse (replace 'h' with 'r')  
rorse -> rose (remove 'r')  
rose -> ros (remove 'e')  

Example 2:  
Input: word1 = "intention", word2 = "execution"  
Output: 5  
Explanation:   
intention -> inention (remove 't')  
inention -> enention (replace 'i' with 'e')  
enention -> exention (replace 'n' with 'x')  
exention -> exection (replace 'n' with 'c')  
exection -> execution (insert 'u')  

Constraints:  
0 <= word1.length, word2.length <= 500  
word1 and word2 consist of lowercase English letters.  

``` cpp
class Solution {
public:
    int minDistance(string word1, string word2) {
        int m=word1.length(),n=word2.length();
        int dp[n+1];
        for(int i=0;i<n+1;i++) dp[i]=i;
        for(int i=0;i<m;i++){
            int tmp=dp[0];
            dp[0]=i+1;
            for(int j=0;j<n;j++){
                if (word1[i]==word2[j]) swap(tmp,dp[j+1]);
                else {
                    int a=tmp;
                    tmp=dp[j+1];
                    dp[j+1]=min({a,dp[j],dp[j+1]})+1;
                }
            }
        }
        return dp[n];
    }
};
```
