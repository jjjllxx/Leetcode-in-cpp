# 242. Valid Anagram
https://leetcode-cn.com/problems/valid-anagram/  
Given two strings s and t, return true if t is an anagram of s, and false otherwise.  
An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.  

Example 1:    
Input: s = "anagram", t = "nagaram"   
Output: true  

Example 2:  
Input: s = "rat", t = "car"  
Output: false  

Constraints:  
1 <= s.length, t.length <= 5 * 10^4  
s and t consist of lowercase English letters.  

Follow up: What if the inputs contain Unicode characters? How would you adapt your solution to such a case?  

``` cpp
class Solution {
public:
    bool isAnagram(string s, string t) {
        vector<int> d(26);
        for(char ch:s) d[ch-'a']++;
        for(char ch:t) d[ch-'a']--;
        for(int i=0;i<26;i++){
            if (d[i]!=0) return false;
        }
        return true;
    }
};
```
