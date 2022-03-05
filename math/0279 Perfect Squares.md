# 279. Perfect Squares
https://leetcode-cn.com/problems/perfect-squares/  
Given an integer n, return the least number of perfect square numbers that sum to n.  
A perfect square is an integer that is the square of an integer; in other words, it is the product of some integer with itself. For example, 1, 4, 9, and 16 are perfect squares while 3 and 11 are not.

Example 1:  
Input: n = 12  
Output: 3  
Explanation: 12 = 4 + 4 + 4.  

Example 2:  
Input: n = 13  
Output: 2  
Explanation: 13 = 4 + 9.  

Constraints:
1 <= n <= 10^4

``` cpp
class Solution {
public:
    bool isPerfectSquare(int x){
        int y=sqrt(x);
        return y*y==x;
    }
    bool isAnswer4(int x){
        while (x%4==0) x/=4;
        return x%8==7;
    }

    int numSquares(int n) {
        if (isPerfectSquare(n)) return 1;
        if (isAnswer4(n)) return 4;
        for (int i=1; i*i<n;i++){
            if (isPerfectSquare(n-i*i)) return 2;
        }
        return 3;
    }
};
```
