# Binary Indexed Tree (BIT)
Use several small intervals to merge as a big interval.

## discretization
``` cpp
// Modify the original vector
void discretise(vector<int>& nums)
{
    sort(nums.begin(), nums.end());
    nums.erase(unique(nums.begin(), nums.end()), nums.end());
}
// Generate a new vector
vector<int> discretise(const vector<int>& nums)
{
    vector<int> ans(nums.begin(), nums.end())
    sort(ans.begin(), ans.end());
    ans.erase(unique(ans.begin(), ans.end()), ans.end());
    return ans;
}
```

## BIT for calculating sum
``` cpp
class BIT {
private:
    std::vector<long long> tree;
public:
    BIT(int n) : tree(n, 0){}

    void update(int i, long long val) {
        while (i <= tree.size()) {
            tree[i] += val;
            i += i & -i;
        }
    }

    long long query(int i) {
        int sum = 0;
        while (i > 0) {
            sum += tree[i];
            i &= i - 1;
        }
        return sum;
    }
};
```

## BIT for find maximum
``` cpp
class BIT {
private:
    std::vector<long long> tree;
public:
    BIT(int n) : tree(n, LLONG_MIN){}

    void update(int i, long long val) {
        while (i <= tree.size()) {
            tree[i] = max(tree[i], val);
            i += i & -i;
        }
    }

    long long query(int i) {
        long long mx = LLONG_MIN;
        while (i > 0) {
            mx = max(mx, tree[i]);
            i &= i - 1;
        }
        return mx;
    }
};
```