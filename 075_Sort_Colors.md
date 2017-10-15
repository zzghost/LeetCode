# Sort Colors
## Description
Given an array with n objects colored red, white or blue, sort them so that objects of the same color are adjacent, with the colors in the order red, white and blue.

Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.

**Note:**
You are not suppose to use the library's sort function for this problem.

**Follow up:**  
A rather straight forward solution is a two-pass algorithm using counting sort.
First, iterate the array counting number of 0's, 1's, and 2's, then overwrite array with total number of 0's, then 1's and followed by 2's.

Could you come up with an one-pass algorithm using only constant space?
## Solution
1. Two-pass  
Count red, white and blue and then arrange them.  
**Complexity: Time O(n), Space O(1).**  
```Java
public void sortColors(int[] nums) {
  int n = nums.length;
  int countOne = 0, countTwo = 0;
  for(int i = 0; i < n; i++){
      sum += nums[i];
      if(nums[i] == 1)
          countOne++;
      if(nums[i] == 2)
          countTwo++;
  }
  int countZero = n - countOne - countTwo;
  for(int i = 0; i < countZero; i++)
      nums[i] = 0;
  for(int i = countZero; i < countZero + countOne; i++)
      nums[i] = 1;
  for(int i = countZero + countOne; i < n; i++)
      nums[i] = 2;
}
```
2. One-pass  
**One pointer.**  
Use `flag` to mark the current arrange color.  
**Complexity: Time O(n), Space O(1).**
```java
public void sortColors(int[] nums) {
    int n = nums.length;
    int flag = 0;
    for(int i = 0, p = 0; p < n && flag != 2; i++){
        if(i == n){
            i = p;
            flag++;
        }
        if(nums[i] == 0){
            int tmp = nums[p];
            nums[p++] = nums[i];
            nums[i] = tmp;
        }
        if(nums[i] == 1 && flag == 1){
            int tmp = nums[p];
            nums[p++] = nums[i];
            nums[i] = tmp;
        }
      }
}
```
**Two pointers.**  
After thinking of the solution above, we can also come up with the idea that use 2 sliding windows.  
Then we use Two pointers.  
Put `0` at start and `2` at end.  
```java
public void sortColors(int[] nums) {
    int n = nums.length;
    int start = 0, end = n - 1, i = 0;
    while(i <= end){
        if(nums[i] == 0){
            nums[i] = nums[start];
            nums[start++] = 0;
        }
        if(nums[i] == 2){
            nums[i] = nums[end];
            nums[end--] = 2;
            i--;
        }
        i++;
    }
}
```
