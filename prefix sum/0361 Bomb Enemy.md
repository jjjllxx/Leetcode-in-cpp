# 361. Bomb Enemy
https://leetcode-cn.com/problems/bomb-enemy/   
Given an m x n matrix grid where each cell is either a wall 'W', an enemy 'E' or empty '0', return the maximum enemies you can kill using one bomb. You can only place the bomb in an empty cell.  
The bomb kills all the enemies in the same row and column from the planted point until it hits the wall since it is too strong to be destroyed.  

Example 1:  
![image](https://user-images.githubusercontent.com/60777462/157157109-7430db29-4a12-4d24-8635-8054ee9ef34b.png)  
Input: grid = [["0","E","0","0"],["E","0","W","E"],["0","E","0","0"]]  
Output: 3  

Example 2:  
![image](https://user-images.githubusercontent.com/60777462/157157137-856e70bd-f543-4c9f-b3b0-641146da82ce.png)  
Input: grid = [["W","W","W"],["0","0","0"],["E","E","E"]]  
Output: 1  

Constraints:  
m == grid.length  
n == grid[i].length  
1 <= m, n <= 500  
grid[i][j] is either 'W', 'E', or '0'.  

``` cpp
class Solution {
public:
    int maxKilledEnemies(vector<vector<char>>& grid) {
        int m=grid.size(),n=grid[0].size(),pre=0,ans=0;
        vector<vector<int>> dp(m,vector<int>(n,0));
        for(int i=0;i<m;i++){
            pre=0;
            for(int j=0;j<n;j++){
                if (grid[i][j]=='W') pre=0;
                else if(grid[i][j]=='E') pre++;
                dp[i][j]+=pre;
            }
            pre=0;
            for(int j=n-1;j>=0;j--){
                if (grid[i][j]=='W') pre=0;
                else if(grid[i][j]=='E') pre++;
                dp[i][j]+=pre;
            }
        }
        for(int j=0;j<n;j++){
            pre=0;
            for(int i=0;i<m;i++){
                if (grid[i][j]=='W') pre=0;
                else if(grid[i][j]=='E') pre++;
                dp[i][j]+=pre;
            }
            pre=0;
            for(int i=m-1;i>=0;i--){
                if (grid[i][j]=='W') pre=0;
                else if(grid[i][j]=='E') pre++;
                dp[i][j]+=pre;
            }
        }
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if (grid[i][j]=='0') ans=max(ans,dp[i][j]);
            }
        }
        return ans;
    }
};
```
