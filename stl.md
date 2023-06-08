# Containers
## std::priority_queue
1. File to include
``` cpp
#include <queue>
```
2. Define priority queue
``` cpp
// Max priority queue, front element is the maximun(default)/
std::priority_queue<int> pq; 

// Min priority queue
std::priority_queue<int, std::vector<int>, std::greater<int>> pq; 

// Using lambda to compare elements.
auto cmp = [](const int a, const int b) 
{ 
    // When this statement return true, a has a high priority before b.
    return (a ^ 1) < (b ^ 1); 
};
std::priority_queue<int, std::vector<int>, decltype(cmp)> pq(cmp);
```
3. Functions
``` cpp
std::priority_queue<int> pq;
pq.top() // accesses the top element
pq.push() // inserts element and sorts the underlying container
pq.emplace() // constructs element in-place and sorts the underlying container
pq.pop() // removes the top element
```

## std::set & std::unordered_set
1. Define a set
``` cpp
std::set<int> st; // default: smaller element is put in the front
std::set<int, std::greater<int>> st; // greater element is put in the front

// costum comparison
struct Point { double x, y; };
struct PointCmp {
    bool operator()(const Point& lhs, const Point& rhs) const { 
        return std::hypot(lhs.x, lhs.y) < std::hypot(rhs.x, rhs.y); 
    }
};

std::set<Point, PointCmp> z = {{2, 5}, {3, 4}, {1, 1}};
z.insert({1, -1}); // this fails because the magnitude of 1,-1 equals 1,1
```

2. Operation for set and unordered_set
``` cpp
std::unordered_set<int> ust;

ust.insert(1);
ust.emplace(2);
const bool isFound = (ust.find(1) != ust.end())
ust.erase(2);
```

3. Operation only for set
``` cpp
std::set<int> st = {1, 2, 4, 5, 8, 10, 12};
const int lb4 = *st.lower_bound(4); // returns an iterator to the first element not less than the given key -> 4
const int ub4 = *st.upper_bound(4); // returns an iterator to the first element greater than the given key -> 5;
```

## std::map & std::unordered_map
## std::multiset & std::multimap
## std::upper_bound & std::lower_bound

# Functions
## std::hypot
``` cpp
#include<cmath>
std::hypot(x, y); // return the square root of (x * x + y * y) 
std::hypot(x, y, z); // return the square root of (x * x + y * y + z * z) 
```
## std::distance
