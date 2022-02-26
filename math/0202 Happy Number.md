# 202. Happy Number
https://leetcode-cn.com/problems/happy-number/  
Write an algorithm to determine if a number n is happy.

A happy number is a number defined by the following process:  
Starting with any positive integer, replace the number by the sum of the squares of its digits.  
Repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1.  
Those numbers for which this process ends in 1 are happy.  
Return true if n is a happy number, and false if not.  

Example 1:  
Input: n = 19  
Output: true  
Explanation:  
1^2 + 9^2 = 82  
8^2 + 2^2 = 68  
6^2 + 8^2 = 100  
12 + 0^2 + 0^2 = 1  

Example 2:  
Input: n = 2  
Output: false  

Constraints:  
1 <= n <= 2^31 - 1  

# two pointer
``` cpp
class Solution {
public:
    int happy(int n){
        int res=0,mod=0;
        while(n){
            mod=n%10;
            res+=mod*mod;
            n/=10;
        }
        return res;
    }

    bool isHappy(int n) {
        int fast=happy(n),slow=n;
        while(fast!=1 && slow!=fast){
            slow=happy(slow);
            fast=happy(happy(fast));
        }
        return fast==1;
    }
};
```
