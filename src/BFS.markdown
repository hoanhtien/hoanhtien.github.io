---
layout: page
title: BFS
permalink: /bfs/
---

# Breadth first search

## Basic implementation

```cpp
#define pb push_back

class Graph {
private:
  int n;
  vector<vector<int>> adj;
  
public:
  Graph(int n) : n(n) { adj.resize(n); }
  
  void addEdge(int u, int v) {
    adj[u].pb(v);
    adj[v].pb(u);
  }
  
  vector<int> distanceFrom(const vector<int>& starts) {
    vector<int> dist(n, -1);
    queue<int> q;
    for (int i : starts) {
      dist[i] = 0;
      q.push(i);
    }
    while (!q.empty()) {
      int i = q.front();
      q.pop();
      for (int j : adj[i]) if (dist[j] == -1) {
        dist[j] = dist[i] + 1;
        q.push(j);
      }
    } 
    return dist;
  }
};
```

## Application
Given a matrix consists of 0 and 1, find the distance of the nearest 0 for each cell. The distance between two adjacent cells is 1.

```cpp
#define range(i,a,b) for (int i=int(a); i<int(b); ++i)
#define id(i, j) (i) * n + (j)

vector<vector<int>> updateMatrix(vector<vector<int>>& matrix) {
  int m = matrix.size(), n = matrix[0].size();
  
  Graph g(m*n);
  range(i,0,m) range(j,0,n) {
    if (i+1 < m) g.addEdge(id(i, j), id(i+1, j));
    if (j+1 < n) g.addEdge(id(i, j), id(i, j+1));
  }
  
  vector<int> zeroes;
  range(i,0,m) range(j,0,n) {
    if (matrix[i][j] == 0) zeroes.pb(id(i, j));
  }
  
  vector<int> distance = g.distanceFrom(zeroes);
  
  vector<vector<int>> res(m, vector<int>(n));
  range(i,0,m) range(j,0,n) res[i][j] = distance[id(i, j)];
  return res;
}
```