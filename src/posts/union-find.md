---
layout: default 
title: Union Find
nav_order: 5
---
# Union find

## Basic implementation
```cpp
class UnionFind {
 private:
  vector<int> p;
  int cnt;

 public:
  UnionFind(int n) {
    p.resize(n, -1);
    cnt = n;
  }

  int Find(int u) {
    int root = u;
    while (p[root] != -1) root = p[root];
    while (u != root) {
      int tmp = p[u];
      p[u] = root;
      u = tmp;
    }
    return root;
  }

  void Union(int u, int v) {
    u = Find(u);
    v = Find(v);
    if (u != v) {
      p[v] = u;
      --cnt;
    }
  }
  
  int Count() {
    return cnt;
  }
};
```

## Example: Number of islands
```cpp
int numIslands(vector<vector<char>>& grid) {
  int m = grid.size(), n = grid[0].size(), res = 0;

  auto id = [n] (int i, int j) { return i * n + j; };

  auto inside = [m, n] (int i, int j) {
    return i >= 0 && j >= 0 && i < m && j < n;
  };

  auto neighbours = [&] (int i, int j) {
    vector<pair<int, int>> res;
    res.reserve(4);
    for (int k = 0; k < 4; ++k) {
      int u = i + deltaRow[k], v = j + deltaCol[k];
      if (inside(u, v) && grid[u][v] == '1')
        res.emplace_back( u, v );
    }
    return res;
  };

  UnionFind uf(m * n);

  for (int i = 0; i < m; ++i) {
    for (int j = 0; j < n; ++j) {
      if (grid[i][j] == '1') {
        for (auto p : neighbours(i, j))
          uf.Union( id(i, j), id(p.first, p.second) );
      }
      else
        --res;
    }
  }

  return res + uf.Count();
}
```