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
