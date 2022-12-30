# Given Q queries, for each query we need to find sum

# Input: 
```md
10
1 2 3 4 5 6 7 8 9 10
5
1 5
2 4
3 9
4 8
5 10
```

# Output:
```md
20
12
49
35
33
```

# Explanation:
1. Approach 1: Brute Force
    - Here we will iterate over the array from l to r and add all the elements in the sum variable. As we have to do this for each query, so the time complexity will be O(n*q). can we do better than this? Yes. We can use prefix sum array to solve this problem in O(1) time. 

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
        int l, r;
        cin >> l >> r;
        int sum = 0;
        for (int i = l - 1; i < r; i++)
        {
            sum += arr[i];
        }
        cout << sum << endl;
    }
    return 0;
}
```

2. Approach 2: Prefix Sum Array
    - Here we will create a prefix sum array and then for each query we will find the sum by subtracting the prefix sum of l-1 from the prefix sum of r. 

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
    int prefix[n];
    prefix[0] = arr[0];
    for (int i = 1; i < n; i++)
    {
        prefix[i] = prefix[i - 1] + arr[i];
    }
    int q;
    cin >> q;
    while (q--)
    {
        int l, r;
        cin >> l >> r;
        if (l == 0){
            cout << prefix[r] << endl;
            continue;
        }
        int sum = prefix[r] - prefix[l - 1];
        cout << sum << endl;
    }

    return 0;
}
```

3. Approach 3: Prefix Sum Array (Optimized)
    - use the same approach as in Approach 2 but instead of creating a prefix sum array, we will create a prefix sum array in the same array.

    - Time Complexity: O(n+q)
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
    for (int i = 1; i < n; i++)
    {
        arr[i] = arr[i - 1] + arr[i];
    }
    int q;
    cin >> q;
    while (q--)
    {
        int l, r;
        cin >> l >> r;
        if (l == 0){
            cout << arr[r] << endl;
            continue;
        }
        int sum = arr[r] - arr[l - 1];
        cout << sum << endl;
    }

    return 0;
}
```