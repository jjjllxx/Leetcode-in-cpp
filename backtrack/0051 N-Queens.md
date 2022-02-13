# 51. N-Queens
https://leetcode-cn.com/problems/n-queens  
The n-queens puzzle is the problem of placing n queens on an n x n chessboard such that no two queens attack each other.  
Given an integer n, return all distinct solutions to the n-queens puzzle. You may return the answer in any order.  
Each solution contains a distinct board configuration of the n-queens' placement, where 'Q' and '.' both indicate a queen and an empty space, respectively.  

Example 1:  
![image](https://user-images.githubusercontent.com/60777462/153738701-3114dcc8-9d38-43a3-b018-91f617e08f0e.png)  
Input: n = 4  
Output: [[".Q..","...Q","Q...","..Q."],["..Q.","Q...","...Q",".Q.."]]  
Explanation: There exist two distinct solutions to the 4-queens puzzle as shown above  

Example 2:  
Input: n = 1  
Output: [["Q"]]  

Constraints:  
1 <= n <= 9  

``` cpp
class Solution {
public:
    vector<vector<string>> ans;
    vector<string> stk;
    vector<bool> row, col, first, second;

    void backtrack(int now, int n,int x){
        if (now==n){
            ans.emplace_back(stk);
            return;
        }
        for (int i=x+1;i<n;i++){
            for (int j=0;j<n;j++){
                if (!((row[i]) || (col[j]) || (first[i-j+n-1]) || (second[i+j]))){
                    row[i]=true;col[j]=true;first[i-j+n-1]=true;second[i+j]=true;
                    stk[i][j]='Q';
                    backtrack(now+1,n,i);
                    stk[i][j]='.';
                    row[i]=false;col[j]=false;first[i-j+n-1]=false;second[i+j]=false;
                }
            }
        }
    }

    vector<vector<string>> solveNQueens(int n) {
        stk.resize(n,string(n,'.'));
        row.resize(n,false);col.resize(n,false);first.resize(2*n-1,false);second.resize(2*n-1,false);
        
        backtrack(0,n,-1);
        return ans;
    }
};
```
