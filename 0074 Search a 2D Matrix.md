# 74. Search a 2D Matrix
https://leetcode-cn.com/problems/search-a-2d-matrix   
Write an efficient algorithm that searches for a value target in an m x n integer matrix matrix. This matrix has the following properties:  
Integers in each row are sorted from left to right.  
The first integer of each row is greater than the last integer of the previous row.  

Example 1:  
![image](https://user-images.githubusercontent.com/60777462/153980911-74f7b5e2-e895-4e64-ad08-776803eee162.png)  
Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3   
Output: true  

Example 2:  
![image](https://user-images.githubusercontent.com/60777462/153980973-61593e9e-2cb3-49ad-9109-9fbeac181981.png)  
Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 13  
Output: false  
 
Constraints:  
m == matrix.length   
n == matrix[i].length  
1 <= m, n <= 100  
-104 <= matrix[i][j], target <= 10^4  

``` cpp
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int i=0,j=matrix[0].size()-1;
        while (i<matrix.size() && j>=0){
            if (matrix[i][j]==target) return true;
            if (matrix[i][j]<target) i++;
            else j--;
        }
        return false;
    }
};
```
