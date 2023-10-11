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