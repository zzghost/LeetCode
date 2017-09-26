# Intersection of Two Arrays II
## Description
Given two arrays, write a function to compute their intersection.  

## Example
Given nums1 = [1, 2, 2, 1], nums2 = [2, 2], return [2, 2].  

**Note:**
1. Each element in the result should appear as many times as it shows in both arrays.
2. The result can be in any order.
**Follow up:**
1. What if the given array is already sorted? How would you optimize your algorithm?
2. What if nums1's size is small compared to nums2's size? Which algorithm is better?
3. What if elements of nums2 are stored on disk, and the memory is limited such that you cannot load all elements into the memory at once?
## Solution
**Complexity: Time O(nlogn), Space O(1)```

```java
public int[] intersect(int[] nums1, int[] nums2) {
    if(nums1 == null || nums1.length == 0)
        return nums1;
    if(nums2 == null || nums2.length == 0)
        return nums2;

    List<Integer> aList = new ArrayList<>();
    Arrays.sort(nums1);Arrays.sort(nums2);
    for(int i = 0, j = 0; i < nums1.length && j < nums2.length;){
        if(nums1[i] == nums2[j]){
            aList.add(nums1[i]);
            i++;j++;
        }
        else if(nums1[i] < nums2[j])
            i++;
        else
            j++;
    }

    int[] result = new int[aList.size()];
    for(int i = 0; i < aList.size(); i++){
        result[i] = (int)aList.get(i);
    }
    return result;
}
```
