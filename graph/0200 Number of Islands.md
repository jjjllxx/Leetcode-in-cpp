# 200. Number of Islands
https://leetcode-cn.com/problems/number-of-islands  
Given an m x n 2D binary grid grid which represents a map of '1's (land) and '0's (water), return the number of islands.

An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

Example 1:  
Input: grid = [  
  ["1","1","1","1","0"],  
  ["1","1","0","1","0"],  
  ["1","1","0","0","0"],  
  ["0","0","0","0","0"]  
]  
Output: 1  

Example 2:  
Input: grid = [  
  ["1","1","0","0","0"],  
  ["1","1","0","0","0"],  
  ["0","0","1","0","0"],  
  ["0","0","0","1","1"]  
]  
Output: 3 
 

Constraints:
m == grid.length  
n == grid[i].length  
1 <= m, n <= 300  
grid[i][j] is '0' or '1'.  

## DFS
```cpp
class Solution {
private:
    static constexpr int dx[4]={1,-1,0,0}, dy[4]={0,0,1,-1};

public:
    int m,n;
    void dfs(vector<vector<char>>& grid,int x, int y){
        grid[x][y]='0';
        for(int i=0;i<4;i++){
            int ax=x+dx[i], ay=y+dy[i];
            if (ax>=m || ax<0 || ay>=n || ay<0) continue;
            if (grid[ax][ay]=='1') dfs(grid,ax,ay); 
        }
    }
    int numIslands(vector<vector<char>>& grid) {
        int ans=0;
        m=grid.size(),n=grid[0].size();
        for(int i=0; i<m; i++){
            for(int j=0; j<n; j++){
                if (grid[i][j]=='1'){
                    ans++;
                    dfs(grid,i,j);
                }
            }
        }
        return ans;
    }
};
```

## BFS
``` cpp
class Solution {
public:
    int numIslands(vector<vector<char>>& grid) {
        queue<pair<int, int>> que;
        int m=grid.size(),n=grid[0].size(),ans=0;
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if (grid[i][j]=='1'){
                    ans++;que.push({i,j});
                    grid[i][j]='0';
                    while(!que.empty()){
                        auto a=que.front();
                        que.pop();
                        int x=a.first,y=a.second;
                        if (x-1>=0 && grid[x-1][y]=='1'){
                            grid[x-1][y]='0';
                            que.push({x-1,y});
                        }
                        if (y-1>=0 && grid[x][y-1]=='1'){
                            grid[x][y-1]='0';
                            que.push({x,y-1});
                        }
                        if (x+1<m && grid[x+1][y]=='1'){
                            grid[x+1][y]='0';
                            que.push({x+1,y});
                        }
                        if (y+1<n && grid[x][y+1]=='1'){
                            grid[x][y+1]='0';
                            que.push({x,y+1});
                        }     
                    }
                }
            }
        }
        return ans;
    }
};
```
