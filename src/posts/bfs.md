---
layout: default 
title: BFS
nav_order: 4
---
# Breadth first search

## Basic implementation
Calculate the shortest distance from every vertex to a set of staring vertices.
```cpp
class Graph {
 private:
  int n;
  vector<vector<int>> adj;
  vector<int> dist;

 public:
  Graph(int n) : n(n) {
    adj.resize(n);
    dist.resize(n, -1);
  }

  void AddEdge(int u, int v) {
    adj[u].push_back(v);
    adj[v].push_back(u);
  }

  void Bfs(int start) {
    queue<int> q;
    dist[start] = 0;
    q.push(start);
     
    while (!q.empty()) {
      int u = q.front();
      q.pop();
      for (int v : adj[u]) if (dist[v] == -1) {
        dist[v] = dist[u] + 1;
        q.push(v);
      }
    }
  }
  
  int Distance(int u) {
    return dist[u];
  }
};
```

## Example: Number of islands
```cpp
int numIslands(vector<vector<char>>& grid) {
  int m = grid.size(), n = grid[0].size(), res = 0;
  auto id = [&n] (int i, int j) { return i * n + j; };
  auto is_land = [&grid] (int i, int j) { return grid[i + 1][j] == '1'; };

  Graph g(m*n);

  for (int i = 0; i < m; ++i) {
    for (int j = 0; j < n; ++j) {
      if (grid[i][j] == '1') {
        if (i + 1 < m && grid[i+1][j] == '1')
          g.AddEdge( id(i, j), id(i+1, j) );
        if (j + 1 < n && grid[i][j+1] == '1')
          g.AddEdge( id(i, j), id(i, j+1) );
      }
      else
        --res;
    }
  }

  for (int i = 0; i < m; ++i) {
    for (int j = 0; j < n; ++j) {
      if (g.Distance( id(i, j) ) == -1) {
        g.Bfs( id(i, j) );
        ++res;
      }
    }
  }

  return res;
}
```