# 304. Range Sum Query 2D - Immutable
https://leetcode-cn.com/problems/range-sum-query-2d-immutable/  
Given a 2D matrix matrix, handle multiple queries of the following type:  
Calculate the sum of the elements of matrix inside the rectangle defined by its upper left corner (row1, col1) and lower right corner (row2, col2).  
Implement the NumMatrix class:  

NumMatrix(int[][] matrix) Initializes the object with the integer matrix matrix.  
int sumRegion(int row1, int col1, int row2, int col2) Returns the sum of the elements of matrix inside the rectangle defined by its upper left corner (row1, col1) and lower right corner (row2, col2).  

Example 1:  
![image](https://user-images.githubusercontent.com/60777462/156893161-32c54b1f-99fc-40b6-bfd6-e13f5778db28.png)  
Input  
["NumMatrix", "sumRegion", "sumRegion", "sumRegion"]  
[[[[3, 0, 1, 4, 2], [5, 6, 3, 2, 1], [1, 2, 0, 1, 5], [4, 1, 0, 1, 7], [1, 0, 3, 0, 5]]], [2, 1, 4, 3], [1, 1, 2, 2], [1, 2, 2, 4]]  
Output  
[null, 8, 11, 12]  

Explanation  
NumMatrix numMatrix = new NumMatrix([[3, 0, 1, 4, 2], [5, 6, 3, 2, 1], [1, 2, 0, 1, 5], [4, 1, 0, 1, 7], [1, 0, 3, 0, 5]]);  
numMatrix.sumRegion(2, 1, 4, 3); // return 8 (i.e sum of the red rectangle)  
numMatrix.sumRegion(1, 1, 2, 2); // return 11 (i.e sum of the green rectangle)  
numMatrix.sumRegion(1, 2, 2, 4); // return 12 (i.e sum of the blue rectangle)  

Constraints:  
m == matrix.length  
n == matrix[i].length  
1 <= m, n <= 200  
-10^5 <= matrix[i][j] <= 10^5  
0 <= row1 <= row2 < m  
0 <= col1 <= col2 < n  
At most 104 calls will be made to sumRegion.  

``` cpp
class NumMatrix {
public:
    vector<vector<int>> presum;
    NumMatrix(vector<vector<int>>& matrix) {
        int m = matrix.size(), n = matrix[0].size();
        presum.resize(m + 1, vector<int>(n + 1));
        for (int i = 0; i < m; ++i) {
            for(int j = 0; j < n; ++j) {
                presum[i + 1][j + 1] = matrix[i][j] + presum[i + 1][j] + presum[i][j + 1] -presum[i][j];
            }
        }
    }
    
    int sumRegion(int row1, int col1, int row2, int col2) {
        return presum[row2 + 1][col2 + 1] - presum[row2 + 1][col1] - presum[row1][col2 + 1] + presum[row1][col1];
    }
};

/**
 * Your NumMatrix object will be instantiated and called as such:
 * NumMatrix* obj = new NumMatrix(matrix);
 * int param_1 = obj->sumRegion(row1,col1,row2,col2);
 */
```
