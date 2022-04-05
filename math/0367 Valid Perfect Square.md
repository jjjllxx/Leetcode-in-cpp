# 367. Valid Perfect Square
https://leetcode-cn.com/problems/valid-perfect-square/  
Given a positive integer num, write a function which returns True if num is a perfect square else False.  
Follow up: Do not use any built-in library function such as sqrt.   

Example 1:  
Input: num = 16  
Output: true  

Example 2:   
Input: num = 14  
Output: false  

Constraints:  
1 <= num <= 2^31 - 1  

## binary search
``` cpp
class Solution {
public:
    bool isPerfectSquare(int num) {
        int left = 1, right = num;
        while (left <= right) {
            long long mid = (right - left) / 2 + left;
            if (mid * mid == num) {
                return true;
            }
            if (mid * mid < num) {
                left = mid + 1;
            }
            else {
                right = mid - 1;
            }
        }
        return false;
    }
};
```
