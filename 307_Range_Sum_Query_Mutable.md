# Range Sum Query - Mutable
DescriptionHintsSubmissionsDiscussSolution
Given an integer array nums, find the sum of the elements between indices i and j (i ≤ j), inclusive.

The update(i, val) function modifies nums by updating the element at index i to val.
Example:
```
Given nums = [1, 3, 5]

sumRange(0, 2) -> 9
update(1, 2)
sumRange(0, 2) -> 8
```
**Note:**  
+ The array is only modifiable by the update function.
+ You may assume the number of calls to update and sumRange function is distributed evenly.

## Solution
Segment Tree.    
```java
class NumArray {
    int[] value;
    int rightEnd;
    public void buildSegmentTree(int[] value, int[] nums, int pos, int left, int right){
        if(left == right){
            value[pos] = nums[left];
            return ;
        }
        int mid = (right - left) / 2 + left;
        buildSegmentTree(value, nums, 2 * pos + 1, left, mid);
        buildSegmentTree(value, nums, 2 * pos + 2, mid + 1, right);
        value[pos] = value[2 * pos + 1] + value[2 * pos + 2];
    }
    public int sumRangeSegmentTree(int[] value, int pos, int left, int right, int qleft, int qright){
        if(qleft > right || qright < left){
            return 0;
        }
        if(qleft <= left && qright >= right){
            return value[pos];
        }
        int mid = (right - left) / 2 + left;
        return sumRangeSegmentTree(value, pos * 2 + 1, left, mid, qleft, qright)
            + sumRangeSegmentTree(value, pos * 2 + 2, mid + 1, right, qleft, qright);
    }
    public void updateSegmentTree(int[] value, int pos, int left, int right, int idx, int val){
        if(left == right && left == idx){
            value[pos] = val;
            return ;
        }
        int mid = (right - left) / 2 + left;
        if(idx <= mid){
            updateSegmentTree(value, 2 * pos + 1, left, mid, idx, val);
        }
        else{
            updateSegmentTree(value, 2 * pos + 2, mid + 1, right, idx, val);
        }
        value[pos] = value[2 * pos + 1] + value[2 * pos + 2];
    }
    public NumArray(int[] nums) {
        if(nums.length == 0){
            return ;
        }
        int n = nums.length * 4;
        value = new int[n];
        buildSegmentTree(value, nums, 0, 0, nums.length - 1);
        rightEnd = nums.length - 1;
    }

    public void update(int i, int val) {
        updateSegmentTree(value, 0, 0, rightEnd, i, val);
    }

    public int sumRange(int i, int j) {
        return sumRangeSegmentTree(value, 0, 0, rightEnd, i, j);
    }
}
```
