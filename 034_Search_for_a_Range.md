```java
public int[] searchRange(int[] nums, int target) {
    int[] rst = {-1, -1};
    if(nums == null || nums.length == 0)
        return rst;

    int low = 0, high = nums.length - 1;
    while(low <= high){
        while(low < nums.length && nums[low] < target )
            low++;
        while(high >= 0 && nums[high] > target )
            high--;
        if(low < nums.length && high >= 0 && nums[low] == target && nums[high] == target){
            rst[0] = low;
            rst[1] = high;
            return rst;
        }

    }
    return rst;
}
```
