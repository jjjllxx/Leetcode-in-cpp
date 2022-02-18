# 96. Unique Binary Search Trees
Given an integer n, return the number of structurally unique BST's (binary search trees) which has exactly n nodes of unique values from 1 to n.  

Example 1:  
![image](https://user-images.githubusercontent.com/60777462/154602363-0bc81807-0420-495f-ba5d-24d7a790c4ba.png)  
Input: n = 3  
Output: 5  

Example 2:  
Input: n = 1  
Output: 1  

Constraints:  
1 <= n <= 19  

``` cpp
class Solution {
public:
    int numTrees(int n) {
        vector<int> dp(n+1,0);
        dp[0]=1;
        dp[1]=1;
        for(int i=2;i<=n;i++){
            for(int j=0;j<i;j++){
                dp[i]+=dp[j]*dp[i-j-1];
            }
        }
        return dp.back();
    }
};
```
