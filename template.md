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
