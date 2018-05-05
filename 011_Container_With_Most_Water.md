# Container With Most Water
## Description
Given n non-negative integers a1, a2, ..., an, where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.  

**Note:** You may not slant the container and n is at least 2.  

## Solution
Two pointers.  
Water's volume depends on 1)height(the lower height) 2)width(the two lines' distance)   
**Complexity: Time O(n), Space O(1).**
```java
public int maxArea(int[] height) {
  int n = height.length;
  int rst = 0;
  int start = 0, end = n - 1;
  while(start < end){
      int tmp = Math.min(height[start], height[end]) * (end - start);
      rst = Math.max(rst, tmp);
      if(height[start] >= height[end])
          end--;
      else
          start++;
  }
  return rst;
}
```    
