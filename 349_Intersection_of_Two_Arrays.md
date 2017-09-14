# Intersection of Two Arrays
Given two arrays, write a function to compute their intersection.  

**Example:**  
Given nums1 = [1, 2, 2, 1], nums2 = [2, 2], return [2].  

**Note:**
1. Each element in the result must be unique.  
2. The result can be in any order.  
## Solution
**Complexity: Time O(mlogn), Space O(1).**
```java
public boolean binarySearch(int target, int[] nums){
    int low = 0, high = nums.length - 1;
    while(low < high){
        int mid = (high - low) / 2 + low;
        if(nums[mid] == target)
            return true;
        if(nums[mid] > target)
            high = mid - 1;
        else
            low = mid + 1;
    }
    return (nums[low] == target);
}
public int[] intersection(int[] nums1, int[] nums2) {
    if(nums1 == null || nums1.length == 0)
        return nums1;
    if(nums2 == null || nums2.length == 0)
        return nums2;

    Arrays.sort(nums2);

    HashSet<Integer> rst = new HashSet<>();

    for(int i = 0; i < nums1.length; i++){
        if(binarySearch(nums1[i], nums2)){
            rst.add(nums1[i]);
        }
    }

    int[] result = new int[rst.size()];
    Iterator iter = rst.iterator();
    int i = 0;
    while(iter.hasNext()){
        result[i++] = (int)iter.next();
    }

    return result;
}
```
