# 63. Unique Paths II
https://leetcode-cn.com/problems/unique-paths-ii/  
A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).
The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).
Now consider if some obstacles are added to the grids. How many unique paths would there be?
An obstacle and space is marked as 1 and 0 respectively in the grid.

Example 1:  
![image](https://user-images.githubusercontent.com/60777462/152140947-d2117169-7be2-4b26-9147-fdad6b01f9d2.png)  
Input: obstacleGrid = [[0,0,0],[0,1,0],[0,0,0]]  
Output: 2  
Explanation: There is one obstacle in the middle of the 3x3 grid above.  
There are two ways to reach the bottom-right corner:  
1. Right -> Right -> Down -> Down  
2. Down -> Down -> Right -> Right  

Example 2:  
![image](https://user-images.githubusercontent.com/60777462/152141006-67768b35-af37-411c-aeea-ccbbb3775aac.png)  
Input: obstacleGrid = [[0,1],[0,0]]  
Output: 1  

Constraints:  
m == obstacleGrid.length  
n == obstacleGrid[i].length  
1 <= m, n <= 100  
obstacleGrid[i][j] is 0 or 1.  
``` cpp

class Solution {
public:
    int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) {
        int m=obstacleGrid.size(),n=obstacleGrid[0].size();
        if(obstacleGrid[0][0]||obstacleGrid[m-1][n-1]==1) return 0;
        obstacleGrid[0][0]=1;
        for(int i=1;i<n;i++){
            if (obstacleGrid[0][i]==1){
                obstacleGrid[0][i]=0;
            }
            else{
                obstacleGrid[0][i]=obstacleGrid[0][i-1];
            }
        }
        for(int i=1;i<m;i++){
            if(obstacleGrid[i][0]==1){
                obstacleGrid[i][0]=0;
            }
            else{
                obstacleGrid[i][0]=obstacleGrid[i-1][0];
            }
            for(int j=1;j<n;j++){
                if(obstacleGrid[i][j]==1){
                    obstacleGrid[i][j]=0;
                }
                else{
                    obstacleGrid[i][j]=obstacleGrid[i-1][j]+obstacleGrid[i][j-1];
                }
            }
        }
        return obstacleGrid[m-1][n-1];
    }
};

```
