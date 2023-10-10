# BinarySearch
## lower bound (>= target)
### Method 1
find first element which equals to(greater than) target  
both left and right are closed interval: [left, right]
``` cpp
int findLowerBound(const std::vector<int>& nums, int target)
{
     int left = 0, right = nums.size() - 1; // must use int here to handle -1
     while (left <= right)
     {
         int mid = ((right - left) >> 1) + left; // prevent integer overflow
         if (nums[mid] < target)
         {
             left = mid + 1; // [mid + 1, right]
         }
         else
         {
             right = mid - 1; // [left, mid - 1]
         }
     }

     return left; // right + 1
}
```
Notes:
1. If every element is less than target, return the size of array.
2. If every element is greater than target, return 0.
3. In the final result, left == right + 1.

### Method 2
right is open interval: [left, right)
``` cpp
int findLowerBound(const std::vector<int>& nums, int target)
{
     int left = 0, right = nums.size(); // must use int here to handle -1
     while (left < right) // or left != right
     {
         int mid = ((right - left) >> 1) + left;
         if (nums[mid] < target)
         {
             left = mid + 1; // [mid + 1, right)
         }
         else
         {
             right = mid; // [left, mid)
         }
     }

     return left; // or right
}
```

### Method 3 
Both left and right are open intervals: (left, right)
``` cpp
int findLowerBound(const std::vector<int>& nums, int target)
{
     int left = -1, right = nums.size();
     while (left + 1 < right)
     {
         int mid = ((right - left) >> 1) + left;
         if (nums[mid] < target)
         {
             left = mid; // (mid, right)
         }
         else
         {
             right = mid; // (left, mid)
         }
     }

     return right; // left + 1
}
```
## lower bound(>)
This situation can be transfered to find >= target + 1

## upper bound(<=)
This situation is opposite to find >= target + 1

## upper bound(<)
This situation is opposite to find >= target
