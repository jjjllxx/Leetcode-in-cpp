# 547. Number of Provinces
https://leetcode-cn.com/problems/number-of-provinces  
There are n cities. Some of them are connected, while some are not. If city a is connected directly with city b, and city b is connected directly with city c, then city a is connected indirectly with city c.

A province is a group of directly or indirectly connected cities and no other cities outside of the group.

You are given an n x n matrix isConnected where isConnected[i][j] = 1 if the ith city and the jth city are directly connected, and isConnected[i][j] = 0 otherwise.

Return the total number of provinces.


Example 1:  
<img width="237" alt="image" src="https://user-images.githubusercontent.com/60777462/153696564-314ee26f-78a9-4a48-ad08-dc0b5dbfc3f9.png">  
Input: isConnected = [[1,1,0],[1,1,0],[0,0,1]]  
Output: 2  

Example 2:   
<img width="233" alt="image" src="https://user-images.githubusercontent.com/60777462/153696577-1bc96088-2f98-4768-b60a-8681bcb875d3.png">  
Input: isConnected = [[1,0,0],[0,1,0],[0,0,1]]  
Output: 3   

Constraints:  
1 <= n <= 200  
n == isConnected.length  
n == isConnected[i].length  
isConnected[i][j] is 1 or 0.  
isConnected[i][i] == 1  
isConnected[i][j] == isConnected[j][i]   

## BFS
``` cpp
class Solution {
public:
    int findCircleNum(vector<vector<int>>& isConnected) {
        int n=isConnected.size(),ans=0;
        queue<int> que;
        vector<int> visited(n);
        for(int i=0;i<n;i++){
            if (visited[i]!=1){
                ans++;
                visited[i]=1;
                que.push(i);
                while(!que.empty()){
                    int x=que.front();
                    que.pop();
                    for(int j=0;j<n;j++){
                        if (isConnected[x][j]==1 && visited[j]!=1){
                            visited[j]=1;
                            que.push(j);
                        }
                    }
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
private:
    void dfs(vector<vector<int>>& isConnected,int x,vector<int>& visited){
        int num=isConnected.size();
        for(int j=0;j<num;j++){
            if (isConnected[x][j]==1 and visited[j]!=1){
                visited[j]=1;
                dfs(isConnected,j,visited);
            }
            
        }
    }
public:
    int findCircleNum(vector<vector<int>>& isConnected) {
        int n=isConnected.size(),ans=0;
        vector<int> visited(n);
        for(int i=0;i<n;i++){
            if (visited[i]!=1){
                ans++;
                visited[i]=1;
                dfs(isConnected,i,visited);
            }
        }
        return ans;
    }
};
```
