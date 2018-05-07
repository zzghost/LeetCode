# Count of Smaller Numbers After Self
You are given an integer array nums and you have to return a new counts array. The counts array has the property where `counts[i]` is the number of smaller elements to the right of `nums[i]`

**Example:**  
```
Given nums = [5, 2, 6, 1]

To the right of 5 there are 2 smaller elements (2 and 1).
To the right of 2 there is only 1 smaller element (1).
To the right of 6 there is 1 smaller element (1).
To the right of 1 there is 0 smaller element.
```
Return the array ``[2, 1, 1, 0]``.


## Solution
1. Divide and Conquer  
Do merge sort and use an array to store the counts.  
Because the indexes will change during the sort. So we sort the index and do not change the primitive array.  
Each time when `nums[index[i]] > nums[index[j]]`, we increase the `rightCount`; when `nums[index[i]] <= nums[index[j]]`, we store the `rightCount`.  
**Complexity: Time O(nlogn), Space O(n).**  
```java
class Solution {
    public void merge(int[] nums, int low, int mid, int high,int[] index, int[] count){
        int[] tmp = new int[high - low + 1];
        int i = low, j = mid + 1, k = 0;
        int rightCount = 0;
        while(i <= mid && j <= high){
            if(nums[index[i]] <= nums[index[j]]){
                count[index[i]] += rightCount;
                tmp[k++] = index[i++];
            }
            else{
                tmp[k++] = index[j++];
                rightCount++;
            }
        }
        while(i <= mid){
            count[index[i]] += rightCount;
            tmp[k++] = index[i++];
        }
        while(j <= high){
            tmp[k++] = index[j++];
        }
        for(i = low; i <= high; i++){
            index[i] = tmp[i - low];
        }
    }
    public void mergeSort(int[] nums, int low, int high,int[] index, int[] count){
        if(low < high){
            int mid = (high - low) / 2 + low;
            mergeSort(nums, low, mid, index, count);
            mergeSort(nums, mid + 1, high, index, count);
            merge(nums, low, mid, high, index, count);
        }
    }
    public List<Integer> countSmaller(int[] nums) {
        int n = nums.length;
        int[] index = new int[n];
        int[] count = new int[n];
        for(int i = 0; i < n; i++){
            index[i] = i;
        }

        mergeSort(nums, 0, nums.length - 1, index, count);

        List<Integer> rst = new ArrayList<>();
        for(int c : count){
            rst.add(c);
        }
        return rst;
    }
}
```
2. Binary Search Tree  
Take `[5, 2, 6, 1]` as an example.  
Consider the reverse order: `[1, 6, 2, 5]`:  
`1` has 0 smaller elements beforehand.  
`6` has 1 smaller elements.  
`2` has 1 while `5` has 2 elements.  
Thus, we create a binary search tree and insert each node by reverse order.  
The BST node has a `count` varible which counts the nodes of left subtree and a `val` varible stores the index in `nums` array.  
```java
class Solution {
    class TreeNode{
        int val;
        //the nodes of left subtree
        int count = 0;
        TreeNode left = null;
        TreeNode right = null;
        public TreeNode(int val){
            this.val = val;
        }
    }
    public void insert(TreeNode root, int value, int idx, int[] count, int[] nums){
        if(nums[root.val] < value){
            count[idx] += root.count + 1;
            if(root.right == null){
                root.right = new TreeNode(idx);
            }
            else{
                insert(root.right, value, idx, count, nums);
            }
        }
        else{
            root.count++;
            if(root.left == null){
                root.left = new TreeNode(idx);
            }
            else{
                insert(root.left, value, idx, count, nums);
            }
        }
    }
    public List<Integer> countSmaller(int[] nums) {
        int n = nums.length;
        int[] count = new int[n];
        TreeNode root = new TreeNode(n - 1);
        //insert into the BST
        for(int i = n - 2; i >= 0; i--){
            insert(root, nums[i], i, count, nums);
        }
        List<Integer> rst = new ArrayList<>();
        for(int c : count){
            rst.add(c);
        }
        return rst;
    }
}
```
