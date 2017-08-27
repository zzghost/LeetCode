# Two Sums  
## Description  
Given an array of integers, return indices of the two numbers such that they add up to a specific target.  
You may assume that each input would have exactly one solution, and you may not use the same element twice.  
## Example  
> Given nums = [2, 7, 11, 15], target = 9,  
> Because nums[0] + nums[1] = 2 + 7 = 9,  
> return [0, 1].  
## Solution  
1. Brute Force.  
Complexity:Time O(n^2), Space O(1)  
> public int[] twoSum(int[] nums, int target) {
>       int[] solution = new int[2];
>       for(int i = 0; i < nums.length; i++)
>           for(int j = i + 1; j < nums.length; j++)
>               if(nums[i] + nums[j] == target){
>                   solution[0] = i;
>                   solution[1] = j;
>                   break;
>               }
>        return solution;
>  }  
2. Two-pass Hash.  
Complexity:Time O(n), Space O(n)  
Using HashMap which key is num and value is index.Put all the entries in the map and search element in it while traversal the array.   
> public int[] twoSum(int[] nums, int target) {
>    int[] solution = new int[2];
>    HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
>    for(int i = 0; i < nums.length; i++)
>       map.put(nums[i], i);
>   for(int i = 0; i < nums.length; i++){
>       int idx = -1;
>       if(map.containsKey(target - nums[i]))
>           idx = map.get(target - nums[i]);
>           if(idx != -1 && idx != i){
>               solution[0] = i;
>               solution[1] = idx;
>           }
>       }
>   return solution;
> }  
3. One-pass Hash.  
Complexity:Time O(n), Space O(n)  
Just like solution 2, HashMap is used. The difference is that we put the entry in the map while we search the element.  
We don't need to consider the `[3, 2, 4], target=6, return[0, 0]` situation.
> public int[] twoSum(int[] nums, int target) {
>   HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
>   for(int i = 0; i < nums.length; i++){
>       int idx = -1;
>       if(map.containsKey(target - nums[i])){
>           idx = map.get(target - nums[i]);
>           return new int[]{i, idx};
>       }
>       map.put(nums[i], i);
>   }
>   throw new IllegalArgumentException("No two solutions.");
>   }

