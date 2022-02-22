# 130. Surrounded Regions
https://leetcode-cn.com/problems/surrounded-regions/  
Given an m x n matrix board containing 'X' and 'O', capture all regions that are 4-directionally surrounded by 'X'.  
A region is captured by flipping all 'O's into 'X's in that surrounded region.  

Example 1:  
![image](https://user-images.githubusercontent.com/60777462/155043769-003bfa1a-6b2a-4c0b-85b6-ddb15417b046.png)  
Input: board = [["X","X","X","X"],["X","O","O","X"],["X","X","O","X"],["X","O","X","X"]]  
Output: [["X","X","X","X"],["X","X","X","X"],["X","X","X","X"],["X","O","X","X"]]  
Explanation: Surrounded regions should not be on the border, which means that any 'O' on the border of the board are not flipped to 'X'. Any 'O' that is not on the border and it is not connected to an 'O' on the border will be flipped to 'X'. Two cells are connected if they are adjacent cells connected horizontally or vertically.  

Example 2:  
Input: board = [["X"]]  
Output: [["X"]]  

Constraints:  
m == board.length  
n == board[i].length  
1 <= m, n <= 200  
board[i][j] is 'X' or 'O'.  

``` cpp
class Solution {
public:
    const int dx[4] = {1, -1, 0, 0};
    const int dy[4] = {0, 0, 1, -1};

    void solve(vector<vector<char>>& board) {
        int n=board.size();
        if (n==0) return;
        int m=board[0].size();
        queue<pair<int,int>> que;
        for(int i=0;i<n;i++){
            if (board[i][0]=='O') que.emplace(i,0);
            if (board[i][m-1]=='O') que.emplace(i,m-1);   
        }
        for(int i=1;i<m-1;i++){
            if (board[0][i]=='O') que.emplace(0,i);
            if (board[n-1][i]=='O')que.emplace(n-1,i);
        }
        while(!que.empty()){
            int x=que.front().first,y=que.front().second;
            que.pop();
            board[x][y]='A';
            for (int i=0;i<4;i++){
                int ax=x+dx[i],ay=y+dy[i];
                if (ax<0||ax>=n||ay<0||ay>=m||board[ax][ay]!='O') continue;
                que.emplace(ax,ay);
                board[ax][ay]='A';
            }
        }
        for(int i=0; i<n;i++){
            for(int j=0;j<m;j++){
                if (board[i][j]=='A') {
                    board[i][j]='O';
                }else if(board[i][j]=='O'){
                    board[i][j]='X';
                }    
            }
        }
        return;
    }
};
```
