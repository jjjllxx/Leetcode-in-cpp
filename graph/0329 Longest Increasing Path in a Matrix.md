# 329. Longest Increasing Path in a Matrix
https://leetcode-cn.com/problems/longest-increasing-path-in-a-matrix/  
Given an m x n integers matrix, return the length of the longest increasing path in matrix.  
From each cell, you can either move in four directions: left, right, up, or down. You may not move diagonally or move outside the boundary (i.e., wrap-around is not allowed).  

Example 1:   
![image](https://user-images.githubusercontent.com/60777462/156959037-118974b5-34ce-4b62-a1f6-c8d7370935a4.png)  
Input: matrix = [[9,9,4],[6,6,8],[2,1,1]]  
Output: 4  
Explanation: The longest increasing path is [1, 2, 6, 9].  

Example 2:  
![image](https://user-images.githubusercontent.com/60777462/156959067-fc61a028-f40f-47ff-b4e1-7962eb97d681.png)  
Input: matrix = [[3,4,5],[3,2,6],[2,2,1]]  
Output: 4  
Explanation: The longest increasing path is [3, 4, 5, 6]. Moving diagonally is not allowed.  

Example 3:  
Input: matrix = [[1]]  
Output: 1  

Constraints:  
m == matrix.length  
n == matrix[i].length  
1 <= m, n <= 200  
0 <= matrix[i][j] <= 2^31 - 1
``` cpp
class Solution {
public:
    int m,n;
    vector<vector<int>> dp;
    int d[4]={1,-1,0,0};
    int dfs(vector<vector<int>>& matrix, int x, int y){
        if (dp[x][y]!=0) return dp[x][y];
        int step=1;
        for(int i=0;i<4;i++){
            int ax=x+d[i], ay=y+d[3-i];
            if (ax>=0 && ax<m && ay>=0 && ay<n && matrix[ax][ay]>matrix[x][y]){
                step=max(step, dfs(matrix,ax,ay)+1);
            }
        }
        dp[x][y]=step;
        return dp[x][y];
    }

    int longestIncreasingPath(vector<vector<int>>& matrix) {
        int ans=1;
        m=matrix.size();
        n=matrix[0].size();
        dp=vector<vector<int>> (m, vector<int>(n,0));
        for (int i=0;i<m;i++){
            for (int j=0;j<n;j++){
                ans=max(ans,dfs(matrix,i,j));
            }
        }
        return ans;
    }
};
```
