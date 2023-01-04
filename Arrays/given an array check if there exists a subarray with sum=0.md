# Given an array check if there exists a subarray with sum=0

```md
Input:
12
2 1 0 1 -2 3 4 -1 2 -1 2 -6

Output:
Yes
```

## Approach 1: Brute Force
- General idea: claculate sum of all subarrays and check if any of them is 0
- Time complexity: O(n^3)
- Space complexity: O(1)

Generalized:
<!-- mkae a table  -->
| L | R |
| 0 | [0, N-1] |
| 1 | [1, N-1] |
| i | [i, N-1] |
| N-1 | [N-1, N-1] |

## Solution 1: Brute Force
```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n;
    cin >> n;
    int a[n];
    for (int i = 0; i < n; i++) {
        cin >> a[i];
    }

    bool found = false;
    for (int l = 0; l < n; l++) {
        for (int r = l; r < n; r++) {
            int sum = 0;
            for (int k = l; k <= r; k++) {
                sum += a[k];
            }
            if (sum == 0) {
                found = true;
            }
        }
    }

    if (found) {
        cout << "Yes" << endl;
    } else {
        cout << "No" << endl;
    }
}
```

## Approach 2: Prefix Sum
- Calculate prefix sum of all elements in the array. 
- If the prefix sum is 0, then the subarray from 0 to the current index is 0. 
- If the prefix sum is already present in the array, then the subarray from the index of the previous occurence of the prefix sum to the current index is 0. 
- Time complexity: O(n^2)
- Space complexity: O(n)

## Solution 2: Prefix Sum
```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n;
    cin >> n;
    int a[n];
    for (int i = 0; i < n; i++) {
        cin >> a[i];
    }

    bool found = false;
    int prefix_sum[n];
    prefix_sum[0] = a[0];
    for (int i = 1; i < n; i++) {
        prefix_sum[i] = prefix_sum[i-1] + a[i];
    }

    for (int l = 0; l < n; l++) {
        for (int r = l; r < n; r++) {
            int sum = prefix_sum[r] - prefix_sum[l] + a[l];
            if (sum == 0) {
                found = true;
            }
        }
    }

    if (found) {
        cout << "Yes" << endl;
    } else {
        cout << "No" << endl;
    }
}
```

## Approach 3: Prefix Sum + Hashing 
- Calculate prefix sum of all elements in the array. Create a hash table to store the prefix sum. 
- We can use unordered_set to store the prefix sum.  
- Will keep on adding the prefix sum to the hash table and check if the prefix sum is already present in the hash table. 
- If the prefix sum is 0, then the subarray from 0 to the current index is 0.


- Time complexity: O(n)
- Space complexity: O(n)

## Solution 3: Prefix Sum + Hashing
```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n;
    cin >> n;
    int a[n];
    for (int i = 0; i < n; i++) {
        cin >> a[i];
    }

    bool found = false;
    int prefix_sum[n];
    prefix_sum[0] = a[0];
    for (int i = 1; i < n; i++) {
        prefix_sum[i] = prefix_sum[i-1] + a[i];
    }

    unordered_set<int> s;
    for (int i = 0; i < n; i++) {
        if (prefix_sum[i] == 0 || s.find(prefix_sum[i]) != s.end()) {
            found = true;
            break;
        }
        s.insert(prefix_sum[i]);
    }

    if (found) {
        cout << "Yes" << endl;
    } else {
        cout << "No" << endl;
    }
}
```