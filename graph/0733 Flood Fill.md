# 733. Flood Fill
https://leetcode-cn.com/problems/flood-fill  
An image is represented by an m x n integer grid image where image[i][j] represents the pixel value of the image.  

You are also given three integers sr, sc, and newColor. You should perform a flood fill on the image starting from the pixel image[sr][sc]. 

To perform a flood fill, consider the starting pixel, plus any pixels connected 4-directionally to the starting pixel of the same color as the starting pixel, plus any pixels connected 4-directionally to those pixels (also with the same color), and so on. Replace the color of all of the aforementioned pixels with newColor.

Return the modified image after performing the flood fill.  

 

Example 1:

<img width="562" alt="image" src="https://user-images.githubusercontent.com/60777462/152635229-3626a22f-27b4-4d7b-b4f6-1af0fbb19aa2.png">  

Input: image = [[1,1,1],[1,1,0],[1,0,1]], sr = 1, sc = 1, newColor = 2   
Output: [[2,2,2],[2,2,0],[2,0,1]]  
Explanation: From the center of the image with position (sr, sc) = (1, 1) (i.e., the red pixel), all pixels connected by a path of the same color as the starting pixel (i.e., the blue pixels) are colored with the new color.  
Note the bottom corner is not colored 2, because it is not 4-directionally connected to the starting pixel.  

Example 2:  
Input: image = [[0,0,0],[0,0,0]], sr = 0, sc = 0, newColor = 2  
Output: [[2,2,2],[2,2,2]]  

Constraints:  
m == image.length  
n == image[i].length  
1 <= m, n <= 50  
0 <= image[i][j], newColor < 216  
0 <= sr < m  
0 <= sc < n  


## DFS  
``` cpp
class Solution {
private:
    static constexpr int dx[4]={1,-1,0,0}, dy[4]={0,0,1,-1};
public:
    int m,n,now,aim;
    void dfs(vector<vector<int>>& image, int sr, int sc){
        image[sr][sc]=aim;
        for (int i=0;i<4;i++){
            int x=sr+dx[i], y=sc+dy[i];
            if (x>=m || x<0 || y>=n || y<0) continue;
            if (image[x][y]==now) dfs(image,x,y);
        }
        return;
    }
    vector<vector<int>> floodFill(vector<vector<int>>& image, int sr, int sc, int newColor) {
        now=image[sr][sc];
        if (now!=newColor) {
            aim=newColor;
            m=image.size();
            n=image[0].size();
            dfs(image,sr,sc);
        }
        return image;
    }
};
```
