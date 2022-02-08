# 3. Longest Substring Without Repeating Characters  
https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/

Given a string s, find the length of the longest substring without repeating characters.  

Example 1:  
Input: s = "abcabcbb"  
Output: 3  
Explanation: The answer is "abc", with the length of 3.  

Example 2:  
Input: s = "bbbbb"  
Output: 1  
Explanation: The answer is "b", with the length of 1.  

Example 3:  
Input: s = "pwwkew"  
Output: 3  
Explanation: The answer is "wke", with the length of 3.  
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.  
  
Constraints:  
0 <= s.length <= 5 * 104  
s consists of English letters, digits, symbols and spaces.  

``` cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        unordered_map<char, int> pos;
        s.insert(0,"#");
        int n=s.length(),ans=0,start=0;
        for(int i=0;i<n;i++){
            start=max(pos[s[i]],start);
            ans=max(ans, i-start);
            pos[s[i]]=i;
        }
        return ans;

    }
};

```
