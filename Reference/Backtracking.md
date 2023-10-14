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

## Combination
Select a combination of `k` from `n` can be assumed as a fixed-length subset.  
Time Complexity O(k $C_n^k$). Space Complexity O(k).
### Prune Skill
Assuming `m` of numbers has been selected, then still need to select d = k - m of numbers.
If the number of numbers to be selected is less than d, then can stop considering this situation.

## Permution
Select one element from current set and enter to the situation set without that element.
bt(i, s) -> {bt(i + 1, s - {x0}), bt(i + 1, s - {x1}), bt(i + 1, s - {x2})...}
