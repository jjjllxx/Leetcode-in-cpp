# binary search template

``` cpp
int biSearch() {
    int left, right;
    int ans = left;
    while(left <= right) {
        int mid = (right + left) / 2;
        if (ok(mid)) {
            left = mid + 1;
            ans = mid;
        }
        else {
             right = mid - 1;
        }
    }
    return ans;
```

function ok() means whether current mid is ok to the problem, if it is ok, return true;  
sometimes mid should be long long type, otherwise may overflow.  
