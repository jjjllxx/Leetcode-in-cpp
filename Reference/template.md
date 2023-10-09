## Binary Search
### lower bound (>= target)
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

Variant 1:  
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

Variant 2:  
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
### lower bound(>)
This situation can be transfered to find >= target + 1

### upper bound(<=)
This situation is opposite to find >= target + 1

### upper bound(<)
This situation is opposite to find >= target

## Union Find(Disjoint Set)
``` cpp
std::vector<int> root;
std::vector<int> rank;
void init(const int n)
{
   root.reserve(n);
   rank.reserve(n);
   for (int i = 0; i < n; ++i)
   {
       root[i] = i;
       rank[i] = 1;
   }
}

int find(const int x)
{
   return x == root[x] ? x : (root[x] = find(root[x]));
}

void merge(const int i, const int j)
{
   int x = find(i), y = find(j);
   rank[x] < rank[y] ? root[x] = y : root[y] = x;
   if (rank[x] == rank[y] && x != y)
   {
       rank[x]++;
   }
}
```

## Trie
``` cpp
const int MAXN = 500005
int next[MAXN][26], pos = 1;
std::memset(next[MAXN][26], 0, sizeof(next));

void insert(const std::string& s)
{
   int cur = 1;
   for(const char c : s)
   {
      if (!next[cur][c - 'a'])
      {
         next[cur][c - 'a'] = ++cnt;
      }
      cur = next[cur][c - 'a'];
   }
}

bool findPrefix(const std::string& s)
{
   int cur = 1;
   for(const char c : s)
   {
      if (!next[cur][c - 'a'])
      {
         return false;
      }
      cur = next[cur][c - 'a'];
   }

   return true;
}
```
