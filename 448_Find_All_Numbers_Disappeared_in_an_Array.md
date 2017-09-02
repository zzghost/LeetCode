# Find All Numbers Disappeared in an Array
## Description
Given an array of integers where 1 ≤ a[i] ≤ n (n = size of array), some elements appear twice and others appear once.  

Find all the elements of [1, n] inclusive that do not appear in this array.  

Could you do it without extra space and in O(n) runtime? You may assume the returned list does not count as extra space.  

## Example

> Input:
> `[4,3,2,7,8,2,3,1]`
>
> Output:
> `[5,6]`
## Solution
1. Swapping.(Not-optimal)  
Complexity: Time O(n^2), Space O(1)
```java
public void Swap(int[] nums, int idx){
    while(nums[idx] - 1 != idx){
        int tmp = nums[nums[idx] - 1];
        if(tmp != nums[idx]){
            nums[nums[idx] - 1] = nums[idx];
            nums[idx] = tmp;
        }
        else
            return ;
    }
}
public List<Integer> findDisappearedNumbers(int[] nums) {
    List<Integer> aList = new ArrayList<Integer>();

    for(int i = 0; i < nums.length; i++)
        Swap(nums, i);

    for(int i = 0; i < nums.length; i++)
        if(nums[i] != i + 1)
            aList.add(i + 1);
    return aList;
}
```
2. Add **n** Mark.
`(nums[i]-1)%n` calculate the original number in the array to get the index.  
if number appears, the number on the position will beyond n after adding n.  
Complexity: Time O(n), Space O(1).  
```java
public List<Integer> findDisappearedNumbers(int[] nums) {
    List<Integer> aList = new ArrayList<Integer>();

    int n = nums.length;
    for(int i = 0; i < n; i++)
        nums[(nums[i] - 1) % n] += n;

    for(int i = 0; i < n; i++)
    //add nums[i] > 0 to take overflow situation into account
        if(nums[i] <= n && nums[i] > 0)
            aList.add(i + 1);
    return aList;
}
```
3. Mark the array.  
If number i appears, mark `nums[nums[i]-1]` negtive.  
Traversal the array, if the num on the position `i` is positive, num `i+1` never appears.  
Complexity: Time O(n), Space O(1)
```java
public List<Integer> findDisappearedNumbers(int[] nums) {
    List<Integer> aList = new ArrayList<Integer>();

    int n = nums.length;
    for(int i = 0; i < n; i++){
        int val = Math.abs(nums[i]) - 1;
        if(nums[val] > 0)
            nums[val] = -nums[val];
    }

    for(int i = 0; i < n; i++)
        if(nums[i] > 0)
            aList.add(i + 1);
    return aList;
}
```
