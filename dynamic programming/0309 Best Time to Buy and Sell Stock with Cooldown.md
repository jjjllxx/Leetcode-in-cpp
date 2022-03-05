# 309. Best Time to Buy and Sell Stock with Cooldown
https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/  
You are given an array prices where prices[i] is the price of a given stock on the ith day.  
Find the maximum profit you can achieve. You may complete as many transactions as you like (i.e., buy one and sell one share of the stock multiple times) with the following restrictions:  
After you sell your stock, you cannot buy stock on the next day (i.e., cooldown one day).  
Note: You may not engage in multiple transactions simultaneously (i.e., you must sell the stock before you buy again).  

Example 1:  
Input: prices = [1,2,3,0,2]  
Output: 3  
Explanation: transactions = [buy, sell, cooldown, buy, sell]  

Example 2:  
Input: prices = [1]  
Output: 0  

Constraints:  
1 <= prices.length <= 5000  
0 <= prices[i] <= 1000  

``` cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int n=prices.size();
        if (n<2) return 0;
        int f0=-prices[0],f1=0,f2=0;
        for(int i=1;i<n;i++){
            int newf0=max(f0,f2-prices[i]);
            int newf1=f0+prices[i];
            int newf2=max(f2,f1);
            f0=newf0;
            f1=newf1;
            f2=newf2;
        }
        return max(f1, f2);
    }
};
```
