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
## std::map & std::unordered_map
## std::multiset & std::multimap
## std::upper_bound & std::lower_bound

# Functions
## std::distance
