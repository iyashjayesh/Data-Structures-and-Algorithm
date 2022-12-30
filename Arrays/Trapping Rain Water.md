## Trapping Rain Water [https://leetcode.com/problems/trapping-rain-water/description/](Problem link)

- Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it can trap after raining.

Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
Explanation: The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped.

Constraints:

n == height.length
1 <= n <= 2 * 104
0 <= height[i] <= 105

- Approach: Using leftMax and rightMax array
    - Here we will use two arrays leftMax and rightMax. leftMax[i] will store the maximum height of the bar to the left of the ith bar. Similarly, rightMax[i] will store the maximum height of the bar to the right of the ith bar. Now, the amount of water that can be stored at the ith bar will be min(leftMax[i],rightMax[i]) - height[i]. We will iterate over the array and add the amount of water stored at each bar to the water variable. Finally, we will return the water variable.

    - Time Complexity: (n(leftM) +n(rghtM) +n(water)) (3n) ~ O(n)
    - - we can neglect the lower order terms
    - - we can neglect constant coefficients
    - Space Complexity: O(n)

```cpp
class Solution {
public:
    int trap(vector<int>& height) {
        int n = height.size();

        int leftM[n];
        leftM[0]=height[0];
        for(int i=1;i<n;i++){
            leftM[i] = max(leftM[i-1],height[i]);
        }

        int rightM[n];
        rightM[n-1]=height[n-1];
        for(int i=n-2;i>=0;i--){
            rightM[i] = max(rightM[i+1],height[i]);
        }
        int water=0;
        for(int i=0;i<n;i++){
            water = water + min(leftM[i],rightM[i]) - height[i];
        }

        return water;
    }
};
```

- Approach: Using two pointers
    - Here we will use two pointers left and right. left will point to the first bar and right will point to the last bar. Now, we will check if the height[left] is less than height[right]. If yes, then we will check if height[left] is greater than leftMax. If yes, then we will update leftMax with height[left]. If no, then we will add leftMax - height[left] to the water variable. Similarly, if height[left] is greater than height[right], then we will check if height[right] is greater than rightMax. If yes, then we will update rightMax with height[right]. If no, then we will add rightMax - height[right] to the water variable. Finally, we will return the water variable.

    - Time Complexity: O(n)
    - Space Complexity: O(1)

```cpp
class Solution {
public:
    int trap(vector<int>& height) {
        int n = height.size();
        int left=0,right=n-1;
        int leftMax=0,rightMax=0;
        int water=0;
        while(left<=right){
            if(height[left]<=height[right]){
                if(height[left]>=leftMax){
                    leftMax = height[left];
                }
                else{
                    water = water + leftMax - height[left];
                }
                left++;
            }
            else{
                if(height[right]>=rightMax){
                    rightMax = height[right];
                }
                else{
                    water = water + rightMax - height[right];
                }
                right--;
            }
        }
        return water;
    }
};
```

