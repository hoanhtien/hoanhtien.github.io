---
layout: page
title: DFS
permalink: /dfs/
---
# Depth first search

## Basic implementation
Determine whether two vertices in a graph are connected.
```cpp
#define pb push_back

class Graph {
private:
  int n;
  vector<vector<int>> adj;
  void dfs(int u) {
    visited[u] = true;
    for (int v : adj[u]) if (!visited[v]) dfs(v);
  }
public:
  Graph(int n) : n(n) { adj.resize(n); }
  void addEdge(int u, int v) {
    adj[u].pb(v);
    adj[v].pb(u);
  }
  bool isConnected(int start, int end) {
    vector<bool> visited(n, false);
    dfs(start);
    return visited[end];
  }
};
```

## Application 1: Escape 2D maze
Determine whether it is possible to go from cell (0, 0) to cell (m-1, n-1) in a 2D maze. The maze is represented as a 2D vector of which each cell has a value of either 0 or 1. Value 0 means that cell is walkable and 1 means it is unwalkable.
```cpp
#define range(i,a,b) for (int i=int(a); i<int(b); ++i)
#define id(i,j) (i) * n + (j)

bool canEscape(vector<vector<int>> maze) {
  int m = maze.size(), n = maze[0].size();
  Graph g(m*n);
  range(i,0,m) range(j,0,n) if (maze[i][j] == 0) {
    if (i+1 < m && maze[i+1][j] == 0)
      g.addEdge(id(i, j), id(i+1, j));
    if (j+1 < n && maze[i][j+1] == 0)
      g.addEdge(id(i, j), id(i, j+1));
  }
  return g.isConnected(id(0, 0), id(m-1, n-1));
}
```