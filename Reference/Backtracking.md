# Backtracking
## Subset
### Template 1
For every element, it can be selected or not selected.
``` cpp
void bt(const int          pos,
         const vector<int>& nums,
         vector<int>&       cur)
{
    if (pos == nums.size())
    {
        ans.push_back(cur);
        return;
    }

    bt1(pos + 1, nums, cur);
    cur.push_back(nums[pos]);
    bt1(pos + 1, nums, cur);
    cur.pop_back();
}
```

### Template 2
Consider next element to be selected
``` cpp
void bt(const int          pos,
         const vector<int>& nums,
         vector<int>&       cur)
{
    ans.push_back(cur);

    for (int i = pos; i < nums.size(); ++i)
    {
        cur.push_back(nums[i]);
        bt1(pos + 1, nums, cur);
        cur.pop_back();
    }
}
```
