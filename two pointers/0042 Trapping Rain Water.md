# 42. Trapping Rain Water
https://leetcode-cn.com/problems/trapping-rain-water  
Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it can trap after raining.

Example 1:  
![image](https://user-images.githubusercontent.com/60777462/153572047-5dd74d26-ccf4-4fd4-9ab0-9da0c4349d64.png)  
Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]  
Output: 6    
Explanation: The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped.  

Example 2:  
Input: height = [4,2,0,3,2,5]  
Output: 9  

Constraints:  
n == height.length  
1 <= n <= 2 * 10^4  
0 <= height[i] <= 10^5  

``` cpp
class Solution {
public:
    int trap(vector<int>& height) {
        int left=0,right=height.size()-1,leftmax=height[left],rightmax=height[right],ans=0;
        while(left<right){
            if (leftmax<rightmax){
                left++;
                ans+=max(0,leftmax-height[left]);
                leftmax=max(leftmax,height[left]);
            }else{
                right--;
                ans+=max(0,rightmax-height[right]);
                rightmax=max(rightmax,height[right]);
            }
        }
        return ans;
    }
};
```
