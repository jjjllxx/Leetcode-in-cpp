# 343. Integer Break
https://leetcode-cn.com/problems/integer-break/   
Given an integer n, break it into the sum of k positive integers, where k >= 2, and maximize the product of those integers.  
Return the maximum product you can get.  

Example 1:  
Input: n = 2  
Output: 1  
Explanation: 2 = 1 + 1, 1 × 1 = 1.  

Example 2:  
Input: n = 10  
Output: 36  
Explanation: 10 = 3 + 3 + 4, 3 × 3 × 4 = 36.  

Constraints:  
2 <= n <= 58  

``` cpp
class Solution {
public:
    int integerBreak(int n) {
        if(n<4) return n-1;
        int now,one=1,two=0,three=0;
        for(int i=3;i<=n;i++){
            now=max({two*2, (i-2)*2, (i-3)*3, three*3});
            three=two;
            two=one;
            one=now;
        }
        return now;
    }
};
```
