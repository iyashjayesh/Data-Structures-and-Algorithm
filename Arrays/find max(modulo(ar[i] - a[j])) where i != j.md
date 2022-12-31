# Given an array of n elements, we have to find `max | ar[i] - a[j] |` where `i != j`

find `max | ar[i] - a[j] |` where `i != j`

input:
```md
8
-3 6 8 2 7 10 -10 5
```

output:
```md
20
```

# Explanation:
- Here we will use the concept of prefix and suffix array.
- We will iterate over the array and find the maximum element from the left side of the array and store it in the prefix array.
- We will iterate over the array in reverse order and find the maximum element from the right side of the array and store it in the suffix array.
- Now we will iterate over the array and find the maximum difference between the current element and the maximum element from the left side of the array and the maximum element from the right side of the array.
- We will print the maximum difference.

- Time Complexity: O(n)
- Space Complexity: O(n)

# Code:
```cpp
#include<bits/stdc++.h>
using namespace std;

int main(){
    int n;
    cin>>n;
    int arr[n];
    for(int i=0; i<n; i++){
        cin>>arr[i];
    }
    int prefix[n];
    prefix[0] = arr[0];
    for(int i=1; i<n; i++){
        prefix[i] = max(prefix[i-1], arr[i]);
    }
    int suffix[n];
    suffix[n-1] = arr[n-1];
    for(int i=n-2; i>=0; i--){
        suffix[i] = max(suffix[i+1], arr[i]);
    }
    int ans = INT_MIN;
    for(int i=0; i<n; i++){
        ans = max(ans, abs(arr[i]-prefix[i]));
        ans = max(ans, abs(arr[i]-suffix[i]));
    }
    cout<<ans<<endl;
    return 0;
}
```
