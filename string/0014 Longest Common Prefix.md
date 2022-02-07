# 14. Longest Common Prefix
https://leetcode-cn.com/problems/longest-common-prefix  

Write a function to find the longest common prefix string amongst an array of strings.
If there is no common prefix, return an empty string "".


Example 1:  
Input: strs = ["flower","flow","flight"]  
Output: "fl"  

Example 2:  
Input: strs = ["dog","racecar","car"]  
Output: ""  
Explanation: There is no common prefix among the input strings.  
 

Constraints:  
1 <= strs.length <= 200  
0 <= strs[i].length <= 200  
strs[i] consists of only lower-case English letters.  

``` cpp
class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        unsigned long n=strs.size(), l=strs[0].length();
        string ans;
        for(int i=0; i<l;i++){
            char now=strs[0][i];
            for (string s:strs){
                if (i>=s.size() || s[i]!=now) return ans;
            }
            ans.push_back(now);
        }
        return ans;
    }
};
```



