# 522. Longest Uncommon Subsequence II
Given an array of strings strs, return the length of the longest uncommon subsequence between them. If the longest uncommon subsequence does not exist, return -1.   

An uncommon subsequence between an array of strings is a string that is a subsequence of one string but not the others.  

A subsequence of a string s is a string that can be obtained after deleting any number of characters from s.

For example, "abc" is a subsequence of "aebdc" because you can delete the underlined characters in "aebdc" to get "abc". Other subsequences of "aebdc" include "aebdc", "aeb", and "" (empty string).
 

Example 1:   
Input: strs = ["aba","cdc","eae"]  
Output: 3  

Example 2:   
Input: strs = ["aaa","aaa","aa"]  
Output: -1  
 

Constraints:   
2 <= strs.length <= 50  
1 <= strs[i].length <= 10  
strs[i] consists of lowercase English letters.  

## solution
``` cpp
class Solution {
public:
    bool judgeLCS(string s1, string s2) {
        int m = s1.length(), n = s2.length();
        if (m < n) {
            return judgeLCS(s2, s1);
        }
        int pos1 = 0, pos2 = 0;
        while(pos1 < m && pos2 < n) {
            if (s1[pos1++] == s2[pos2]) {
                pos2++;
            }
        }
        return pos2 == n;
    }

    int findLUSlength(vector<string>& strs) {
        int n = strs.size(), ans = -1;
        for (int i = 0; i < n; i++) {
            bool flag = true;
            for (int j = 0; j < n; j++) {
                if (i == j) continue;
                if (judgeLCS(strs[i], strs[j]) && strs[i].length() <= strs[j].length()) {
                    flag = false;
                    break;
                }
            }
            if (flag) {
                ans = max(ans, int(strs[i].length()));
            }
        }
        return ans;
    }
};
```

## test judgeLCS function
``` cpp
bool judgeLCS(string s1, string s2) {
    int m = s1.length(), n = s2.length();
    if (m < n) {
        return judgeLCS(s2, s1);
    }
    int pos1 = 0, pos2 = 0;
    while(pos1 < m && pos2 < n) {
        if (s1[pos1++] == s2[pos2]) {
            pos2++;
        }
    }
    return pos2 == n;
}

int main() {
    std::cout << "Hello World!\n";
    string a = "aaab";
    string b = "aa";
    std::cout << judgeLCS(a, b);
    return 0;
}
```
