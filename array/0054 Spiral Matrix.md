# 54. Spiral Matrix
https://leetcode-cn.com/problems/spiral-matrix  
Given an m x n matrix, return all elements of the matrix in spiral order.  

Example 1:  
![image](https://user-images.githubusercontent.com/60777462/153771967-20309bb9-750b-450a-ba1d-286fcee44c96.png)  
Input: matrix = [[1,2,3],[4,5,6],[7,8,9]]  
Output: [1,2,3,6,9,8,7,4,5]  

Example 2:  
![image](https://user-images.githubusercontent.com/60777462/153771987-7a49c2ad-3a34-42c0-9358-bd600492dd4f.png)  
Input: matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]  
Output: [1,2,3,4,8,12,11,10,9,5,6,7]  
 

Constraints:  

m == matrix.length  
n == matrix[i].length  
1 <= m, n <= 10  
-100 <= matrix[i][j] <= 100  

``` cpp
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        int left=0,right=matrix[0].size()-1,up=0,bottom=matrix.size()-1;
        vector<int> ans;
        while(true){
            for(int j=left;j<=right;j++) ans.emplace_back(matrix[up][j]);
            if (++up>bottom) break;
            for(int i=up;i<=bottom;i++) ans.emplace_back(matrix[i][right]);
            if(--right<left) break;
            for(int j=right;j>=left;j--) ans.emplace_back(matrix[bottom][j]);
            if (--bottom<up) break;
            for(int i=bottom;i>=up;i--) ans.emplace_back(matrix[i][left]);
            if (++left>right) break;
        }
        return ans;
    }
};
```
