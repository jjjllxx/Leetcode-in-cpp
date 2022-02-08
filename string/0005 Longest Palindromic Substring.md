# 5. Longest Palindromic Substring  
https://leetcode-cn.com/problems/longest-palindromic-substring/

Given a string s, return the longest palindromic substring in s.  

Example 1:  
Input: s = "babad"  
Output: "bab"  
Explanation: "aba" is also a valid answer.  

Example 2:  
Input: s = "cbbd"  
Output: "bb"  
 

Constraints:  
1 <= s.length <= 1000  
s consist of only digits and English letters.  

## center extension
``` cpp
class Solution {
public:
    pair<int,int> findLength(int left,int right,const string& s){
        while (left>=0 && right<s.size() && s[left]==s[right]){
            left--;
            right++;
        }
        return {left+1,right-1};
    }
    string longestPalindrome(string s) {
        int n=s.length(),start=0,end=0;
        for (int i=0;i<n;i++){
            auto[left1,right1]=findLength(i,i,s);
            if (right1-left1>end-start){
                start=left1;
                end=right1;
            }
            auto[left2,right2]=findLength(i,i+1,s);
            if (right2-left2>end-start){
                start=left2;
                end=right2;
            }
        }
        return s.substr(start,end-start+1);
    }
};
```

## Manacher
