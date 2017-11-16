# Trapping Rain Water
Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it is able to trap after raining.

For example,
Given `[0,1,0,2,1,0,1,3,2,1,2,1]`, return `6`.
## Solution
1. Traversal.  
From left to right, `start` points to the first element, find the first element x which is larger than `height[start]`.If there is such an element, than count the water till the element x; otherwise, count the water till the heightest element till the element at position n - 1.  
**Complexity: Time O(n^2),Space O(1).**
```java
class Solution {
    public int trap(int[] height) {
        if(height == null || height.length == 0)
            return 0;
        int i = 0, n = height.length, sum = 0;
        while(i < n && height[i] == 0) i++;
        int start = i;
        i = start + 1;
        while(start < n - 1){
            int countSum = 0, tmpMaxHeight = height[i], tmpIdx = i;
            while(i < n && height[i] < height[start]){
                countSum += height[i];
                if(height[i] >= tmpMaxHeight){
                    tmpMaxHeight = height[i];
                    tmpIdx = i;
                }
                i++;
            }
            //If there's an element larger than height[start]
            if(i != n){
                countSum += height[start];
                sum += (i - start) * height[start];
                sum -= countSum;
                start = i;
                i++;
            }
            else{
              //if not, find the largest element
                sum += Math.min(tmpMaxHeight, height[start]) * (tmpIdx - start);
                for(int x = start + 1; x <= tmpIdx; x++)
                    sum -= height[x];
                start = tmpIdx;
                i = start + 1;
            }
        }
        return sum;
    }
}
```
2. Two pointers
p1 points from left, p2 points from right.  
  + if nums[p1] < nums[p2], start from p1:  
      find the first element which is >= nums[p1], count the element between them.
  + otherwise, start from p2:   
      find the first element which is >= nums[p2], count the element between them.  
**Complexity: Time O(n), Space O(1).**
```java
class Solution {
    public int trap(int[] height) {
        if(height == null || height.length == 0)
            return 0;
        int n = height.length, left = 0, right = n - 1, sum = 0;
        while(left < right){
            int leftElement = height[left], rightElement = height[right];
            if(leftElement < rightElement){
                left++;
                while(left < right && leftElement > height[left]){
                    sum += (leftElement - height[left]);
                    left++;
                }
            }
            else{
                right--;
                while(left < right && rightElement > height[right]){
                    sum += (rightElement - height[right]);
                    right--;
                }
            }
        }
        return sum;
    }
}
```
