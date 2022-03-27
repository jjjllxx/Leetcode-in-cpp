# 49. Group Anagrams
https://leetcode-cn.com/problems/group-anagrams  
Given an array of strings strs, group the anagrams together. You can return the answer in any order.  
An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.  

Example 1:  
Input: strs = ["eat","tea","tan","ate","nat","bat"]  
Output: [["bat"],["nat","tan"],["ate","eat","tea"]]  

Example 2:  
Input: strs = [""]  
Output: [[""]]  

Example 3:  
Input: strs = ["a"]  
Output: [["a"]]  
 

Constraints:  
1 <= strs.length <= 10^4  
0 <= strs[i].length <= 100  
strs[i] consists of lowercase English letters.  


## sort & hashtable
``` cpp
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        unordered_map<string, vector<string>> mp;
        for (string s : strs) {
            string tmp = s;
            sort(tmp.begin(), tmp.end());
            mp[tmp].emplace_back(s);
        }
        vector<vector<string>> ans;
        for (auto [k, v] : mp) {
            ans.emplace_back(v);
        }
        return ans;
    }
};
```
