# given Q queries with l,r,x add x to the range from l to r(both inclusive) return the final array

# Input:
```md
10
0 0 0 0 0 0 0 0 0 0
5
2 5 3
3 7 2
1 4 -4
5 8 1
6 9 -3
```

# Output:
```md
0 -4 -1 1 1 6 0 0 -2 -3
```

# Explanation:
1. Approach 1: Brute Force
    - Here we will iterate over the array from l to r and add x to each element. As we have to do this for each query, so the time complexity will be O(n*q). can we do better than this? Yes. We can use prefix sum array to solve this problem in O(1) time. 

    - Time Complexity: O(n*q)
    - Space Complexity: O(1)

```cpp
#include <iostream>
using namespace std;

int main()
{
    int n;
    cin >> n;
    int arr[n];
    for (int i = 0; i < n; i++)
    {
        cin >> arr[i];
    }
    int q;
    cin >> q;
    while (q--)
    {
        int l, r, x;
        cin >> l >> r >> x;
        for (int i = l; i < r + 1; i++)
        {
            arr[i] += x;
        }
    }
    for (int i = 0; i < n; i++)
    {
        cout << arr[i] << " ";
    }
    return 0;
}
```

2. Approach 2: Prefix Sum
    - Here we will use prefix sum array to solve this problem. We will iterate over the array and add x to the lth index and subtract x from the (r+1)th index. After this we will iterate over the prefix sum array and print the final array. 

    - Time Complexity: O(n+q)
    - Space Complexity: O(n)

```cpp
#include <iostream>
using namespace std;

int main()
{
    int n;
    cin >> n;
    int arr[n];
    for (int i = 0; i < n; i++)
    {
        cin >> arr[i];
    }
    int prefix[n] = {0};
    int q;
    cin >> q;
    // while (q--)
    // {
    //     int l, r, x;
    //     cin >> l >> r >> x;
    //     prefix[l] += x;
    //     prefix[r + 1] -= x;
    // }
    for (int i = 0; i < q; i++)
    {
        int l, r, x;
        cin >> l >> r >> x;
        prefix[l] += x;
        prefix[r+1] -= x;
    }
    for (int i = 1; i < n; i++)
    {
        prefix[i] += prefix[i - 1];
    }
    for (int i = 0; i < n; i++)
    {
        cout << prefix[i] << " ";
    }
    return 0;
}
```
<!-- @TODO: need to review this -->
3. Approach 3: Binary Indexed Tree (Fenwick Tree) 
    - Here we will use binary indexed tree to solve this problem. We will iterate over the array and add x to the lth index and subtract x from the (r+1)th index. After this we will iterate over the binary indexed tree and print the final array. 

    - Time Complexity: O(n+q)
    - Space Complexity: O(n)

```cpp
#include <iostream>
using namespace std;

void update(int BIT[], int n, int index, int value)
{
    for (; index <= n; index += index & (-index))
    {
        BIT[index] += value;
    }
}

int query(int BIT[], int index)
{
    int sum = 0;
    for (; index > 0; index -= index & (-index))
    {
        sum += BIT[index];
    }
    return sum;
}

int main()
{
    int n;
    cin >> n;
    int arr[n];
    for (int i = 0; i < n; i++)
    {
        cin >> arr[i];
    }
    int BIT[n + 1] = {0};
    int q;
    cin >> q;
    while (q--)
    {
        int l, r, x;
        cin >> l >> r >> x;
        update(BIT, n, l, x);
        update(BIT, n, r + 1, -x);
    }
    for (int i = 1; i <= n; i++)
    {
        cout << query(BIT, i) << " ";
    }
    return 0;
}
```
