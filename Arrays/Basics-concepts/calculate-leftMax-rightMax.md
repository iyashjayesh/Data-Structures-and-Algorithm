# Calculate LeftMax and RightMax in an array 

## LeftMax 
- LeftMax is the maximum element to the left of the current element.
- It is used to find the maximum element to the left of the current element in O(1) time.

example:
```md
arr[] = {4, 3, 2, 8, 1, 4}
lm[] = {4, 4, 4, 8, 8, 8}  -> increasing order/non-decreasing order
```

```cpp
// code to create left max array
lm[0] = arr[0];
for(int i = 1; i < n; i++){
    lm[i] = max(lm[i-1], arr[i]);
}
```

## RightMax
- RightMax is the maximum element to the right of the current element.
- It is used to find the maximum element to the right of the current element in O(1) time.

example:
```md
arr[] = {4, 3, 2, 8, 1, 4}
rm[] = {8, 8, 8, 8, 4, 4} -> decreasing order/non-increasing order
```

```cpp
// code to create right max array
rm[n-1] = arr[n-1];
for(int i = n-2; i >= 0; i--){
    rm[i] = max(rm[i+1], arr[i]);
}
```

