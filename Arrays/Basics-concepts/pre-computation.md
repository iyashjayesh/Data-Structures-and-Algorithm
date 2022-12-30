# Pre-Computations Methods
- Pre Computations are used to reduce the time complexity of a problem. 
- Pre Computations are used to precompute some values and store them in an array.
- These values are then used to solve the problem in O(1) time.

Types of Pre-Computations 
- Prefix Sum or Cumulative Sum
- Suffix Sum 
- Difference Array 
- Left Max Array & Right Max Array

## 1. Prefix Sum or Cumulative Sum

- Prefix sum is the sum of all the elements from the first element to the last element.
- It is used to find the sum of a subarray in O(1) time.
- It is also used to update a range in O(1) time. 
- It is also used to find the number of elements less than or equal to a given number in a range in O(1) time.

example:
```md
arr[] = {1, 2, 3, 4, 5}
pf[] = {1, 3, 6, 10, 15}
```

```cpp
// code to create prefix sum array
pf[0] = arr[0];
for(int i = 1; i < n; i++){
    pf[i] = pf[i-1] + arr[i];
}
```

## 2. Suffix Sum

- Suffix sum is the sum of all the elements from the last element to the first element.
- It is used to find the sum of a subarray in O(1) time.
- It is also used to update a range in O(1) time.

example:
```md
arr[] = {1, 2, 3, 4, 5}
sf[] = {15, 14, 12, 9, 5}
```

```cpp
// code to create suffix sum array
sf[n-1] = arr[n-1];
for(int i = n-2; i >= 0; i--){
    sf[i] = sf[i+1] + arr[i];
}
```

## 3. Difference Array

- Difference array is the difference between the current element and the previous element. 
- It is used to update a range in O(1) time. 
- It is also used to find the sum of a subarray in O(1) time.

example:
```md
arr[] = {1, 2, 3, 4, 5}
df[] = {1, 1, 1, 1, 1}
```

```cpp
// code to create difference array
df[0] = arr[0];
for(int i = 1; i < n; i++){
    df[i] = arr[i] - arr[i-1];
}
```

## 4. Left Max Array & Right Max Array

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
