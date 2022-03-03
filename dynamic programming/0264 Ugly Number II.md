# 264. Ugly Number II
https://leetcode-cn.com/problems/ugly-number-ii/  
An ugly number is a positive integer whose prime factors are limited to 2, 3, and 5.  
Given an integer n, return the nth ugly number.  

Example 1:  
Input: n = 10  
Output: 12  
Explanation: [1, 2, 3, 4, 5, 6, 8, 9, 10, 12] is the sequence of the first 10 ugly numbers.  

Example 2:  
Input: n = 1  
Output: 1  
Explanation: 1 has no prime factors, therefore all of its prime factors are limited to 2, 3, and 5.  

Constraints:
1 <= n <= 1690

``` cpp
class Solution {
public:
    int nthUglyNumber(int n) {
        int two=0,three=0,five=0;
        vector<int> dp(n);
        dp[0]=1;
        for(int i=1;i<n;i++){
            int num2=dp[two]*2,num3=dp[three]*3,num5=dp[five]*5;
            dp[i]=min({num2,num3,num5});
            if (dp[i]==num2) two++;
            if (dp[i]==num3) three++;
            if (dp[i]==num5) five++;
        }
        return dp[n-1];
    }
};
```
