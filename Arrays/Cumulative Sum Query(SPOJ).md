# Cumulative Sum Query [https://www.spoj.com/problems/CSUMQ/](SPOJ Problem)

## Problem Statement
William Macfarlane wants to look at an array.

You are given a list of N numbers and Q queries. Each query is specified by two numbers i and j; the answer to each query is the sum of every number between the range [i, j] (inclusive).

Note: the query ranges are specified using 0-based indexing.

- Input:
The first line contains N, the number of integers in our list (N <= 100,000). The next line holds N numbers that are guaranteed to fit inside an integer. Following the list is a number Q (Q <= 10,000). The next Q lines each contain two numbers i and j which specify a query you must answer (0 <= i, j <= N-1).

- Output:
For each query, output the answer to that query on its own line in the order the queries were made.

- Example:
```
Input:
3
1 4 1
3
1 1
1 2
0 2

Output:
4
5
6
```

Approach 1: Brute Force

- Time Complexity: O(q * (r - l + 1))
- Space Complexity: O(1)

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n;
    cin >> n;
    int arr[n];
    for (int i = 0; i < n; i++) {
        cin >> arr[i];
    }
    int q;
    cin >> q;
    while (q--) {
        int l, r;
        cin >> l >> r;
        int sum = 0;
        for (int i = l; i <= r; i++) {
            sum += arr[i];
        }
        cout << sum << endl;
    }
    return 0;
}
```

Approach 2: Prefix Sum Array (For more info refer [](pre-computation for sum queries))

- Time Complexity: O(n + q)
- Space Complexity: O(n)

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n;
    cin >> n;
    int arr[n];
    for (int i = 0; i < n; i++) {
        cin >> arr[i];
    }
    int prefix[n];
    prefix[0] = arr[0];
    for (int i = 1; i < n; i++) {
        prefix[i] = prefix[i - 1] + arr[i];
    }
    int q;
    cin >> q;
    while (q--) {
        int l, r;
        cin >> l >> r;
        int sum = prefix[r];
        if (l > 0) {
            sum -= prefix[l - 1];
        }
        cout << sum << endl;
    }
    return 0;
}
```

