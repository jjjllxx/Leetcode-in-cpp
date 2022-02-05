# 1219. Path with Maximum Gold
https://leetcode-cn.com/problems/path-with-maximum-gold  
In a gold mine grid of size m x n, each cell in this mine has an integer representing the amount of gold in that cell, 0 if it is empty.

Return the maximum amount of gold you can collect under the conditions:

Every time you are located in a cell you will collect all the gold in that cell.
From your position, you can walk one step to the left, right, up, or down.
You can't visit the same cell more than once.
Never visit a cell with 0 gold.
You can start and stop collecting gold from any position in the grid that has some gold.
 

Example 1:  
Input: grid = [[0,6,0],[5,8,7],[0,9,0]]   
Output: 24  
Explanation:  
[[0,6,0],  
 [5,8,7],  
 [0,9,0]]  
Path to get the maximum gold, 9 -> 8 -> 7.  

Example 2:  
Input: grid = [[1,0,7],[2,0,6],[3,4,5],[0,3,0],[9,0,20]]  
Output: 28  
Explanation:  
[[1,0,7],  
 [2,0,6],  
 [3,4,5],  
 [0,3,0],  
 [9,0,20]]   
Path to get the maximum gold, 1 -> 2 -> 3 -> 4 -> 5 -> 6 -> 7.  

Constraints:
m == grid.length   
n == grid[i].length  
1 <= m, n <= 15  
0 <= grid[i][j] <= 100  
There are at most 25 cells containing gold.  

## backtrack
``` cpp
class Solution {
private:
    static constexpr int dx[4]={1,-1,0,0}, dy[4]={0,0,1,-1};
public:
    int ans=0;
    int m,n;

    void dfs(vector<vector<int>> grid, int now,int x,int y){
        now+=grid[x][y];
        ans=max(now,ans);
        int tmp = grid[x][y];
        grid[x][y]=0;
        for(int i=0;i<4;i++){
            int ax=x+dx[i], ay=y+dy[i];
            if(ax>=m || ax<0 || ay>=n || ay<0) continue;
            if (grid[ax][ay]==0) continue;
            dfs(grid,now,ax,ay);
        }
        grid[x][y]=tmp;
        return;
    }

    int getMaximumGold(vector<vector<int>>& grid) {
        m=grid.size();
        n=grid[0].size();
        for(int i=0; i<m; i++){
            for(int j=0; j<n; j++){
                if (grid[i][j]!=0){
                    dfs(grid,0,i,j);
                }
            }
        }
        return ans;
    }
};
```

## DFS
``` cpp
class Solution {
public:
    int ans=0;
    int dx[4]={1,-1,0,0}, dy[4]={0,0,1,-1};
    int m,n;
    void dfs(vector<vector<int>>& grid,vector<vector<int>> vis, int now,int x,int y){
        vis[x][y]=1;
        for(int i=0;i<4;i++){
            int ax=x+dx[i], ay=y+dy[i];
            if(ax<0 || ax>=m || ay<0 || ay>=n) continue;
            if (grid[ax][ay]==0 || vis[ax][ay]!=0) continue;
            ans=max(ans,now+grid[ax][ay]);
            dfs(grid,vis,now+grid[ax][ay],ax,ay);
        }
        return;
    }

    int getMaximumGold(vector<vector<int>>& grid) {
        m=grid.size();
        n=grid[0].size();
        for(int i=0; i<m; i++){
            for(int j=0; j<n; j++){
                if (grid[i][j]!=0){
                    vector<vector<int>> vis(m, vector<int>(n,0));
                    ans=max(ans,grid[i][j]);
                    dfs(grid,vis,grid[i][j],i,j);
                }
            }
        }
        return ans;
    }
};
```
