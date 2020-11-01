---
layout: default 
title: DFS
nav_order: 3
---
# Depth first search

## Basic implementation
Determine whether two vertices in a graph are connected.
```cpp
class Graph {
 private:
  int n;
  vector<vector<int>> adj;
  vector<bool> visited;

  void Dfs(int u) {
    visited[u] = true;
    for (int v : adj[u]) if (!visited[v]) Dfs(v);
  }

 public:
  Graph(int n) : n(n) {
    adj.resize(n);
    visited.resize(n, false);
  }

  void AddEdge(int u, int v) {
    adj[u].push_back(v);
    adj[v].push_back(u);
  }

  bool IsConnected(int start, int end) {
    Dfs(start);
    return visited[end];
  }
};
```

## Example: Escape 2D maze
Determine whether it is possible to go from cell (0, 0) to cell (m-1, n-1) in a 2D maze. The maze is represented as a 2D vector of which each cell has a value of either 0 or 1. Value 0 means that cell is walkable and 1 means it is unwalkable.
```cpp
bool canEscape(vector<vector<int>> maze) {
  int m = maze.size(), n = maze[0].size();

  auto id = [&n] (int i, int j) {
    return i * n + j;
  };

  Graph g(m * n);
  for (int i = 0; i < m; ++i) {
    for (int j = 0; j < n; ++j) {
      if (maze[i][j] == 0) {
        if (i + 1 < m && maze[i+1][j] == 0)
          g.AddEdge( id(i, j), id(i + 1, j) );
        if (j + 1 < n && maze[i][j+1] == 0)
          g.AddEdge( id(i, j), id(i, j + 1) );
      }
    }
  }

  return g.IsConnected( id(0, 0), id(m - 1, n - 1) );
}
```