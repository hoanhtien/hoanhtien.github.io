---
layout: default
title: C++ template
nav_order: 2
---
# C++ template for competitive programming
For competitive programming only, do not use at work.
```cpp
typedef long long ll;
typedef pair<int, int> pii;
typedef pair<int, pair<int, int>> piii;

#define watch1(x) cout << #x << ": " << x << endl
#define watch2(x, y) cout << #x << ": " << x << ", " << #y << ": " << y << endl

void Print(char x) { cout << x; }
void Print(int x) { cout << x; }
void Print(ll x) { cout << x; }
void Print(double x) { cout << x; }
void Print(string x) { cout << x; }
void Print(pii x) { cout << "{" << x.first << ", " << x.second << "}"; }

template <class T>
void Print1D(vector<T>& seq, string info="") {
  if (!info.empty())
    cout << info << ":" << endl;
  for (auto& value : seq) {
    Print(value);
    cout << " ";
  }
  cout << endl;
}

template <class T>
void Print1D(T* seq, int n, string info="") {
  if (!info.empty())
    cout << info << ":" << endl;
  for (int i = 0; i < n; ++i) {
    Print(seq[i]);
    cout << " ";
  }
  cout << endl;
}

template <class T>
void Print2D(vector<vector<T>>& matrix, string info="") {
  if (!info.empty())
    cout << info << ":" << endl;
  for (auto& row : matrix) Print1D(row);
}

template <size_t rows, size_t cols, class T>
void Print2D(T matrix[rows][cols], int m, int n, string info="") {
  if (!info.empty())
    cout << info << ":" << endl;
  for (int i = 0; i < m; ++i) Print1D(matrix[i], n);
}
```