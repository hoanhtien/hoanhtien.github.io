---
layout: default
title: C++ template for competitive programming 
nav_order: 2
---

# C++ template for competitive programming
For competitive programming only, do not use at work.
```cpp
typedef long long ll;
typedef pair<int, int> pii;
typedef pair<int, pair<int, int>> piii;

#define watch(x) cout << #x << ": " << x << endl
#define watch(x, y) cout << #x << ": " << x << ", " << #y << ": " << y << endl

template<class C, class T>
void Print1D(string& info, C<T>& seq) {
  cout << info << ":" << endl;
  for (auto& value : seq) cout << value << " ";
  cout << endl;
}

template<class C, class T>
void Print2D(string& info, C<C<T>>& matrix) {
  cout << info << ":" << endl;
  for (auto& row : matrix) Print1D(info, row);
  cout << endl;
}
```