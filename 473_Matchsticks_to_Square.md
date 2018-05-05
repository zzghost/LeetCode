# Matchsticks to Square
## Description
Remember the story of Little Match Girl? By now, you know exactly what matchsticks the little match girl has, please find out a way you can make one square by using up all those matchsticks. You should not break any stick, but you can link them up, and each matchstick must be used exactly one time.

Your input will be several matchsticks the girl has, represented with their stick length. Your output will either be true or false, to represent whether you could make one square using all the matchsticks the little match girl has.

Example 1:
```
Input: [1,1,2,2,2]
Output: true

Explanation: You can form a square with length 2, one side of the square came two sticks with length 1.
```
Example 2:
```
Input: [3,3,3,3,4]
Output: false

Explanation: You cannot find a way to form a square with all the matchsticks.
```
**Note:**  
+ The length sum of the given matchsticks is in the range of 0 to 10^9.
+ The length of the given matchstick array will not exceed 15.

## Solution
1. BackTracking
```java
class Solution {
    public void reverse(int[] nums){
        int n = nums.length;
        for(int i = 0; i < n / 2; i++){
            int tmp = nums[n - i - 1];
            nums[n - i - 1] = nums[i];
            nums[i] = tmp;
        }
    }
    public boolean makeSquare(int idx, int[] nums, int length, int[] bucket){
        if(idx >= nums.length){
            return bucket[0] == length && bucket[1] == length && bucket[2] == length && bucket[3] == length;
        }
        for(int i = 0; i < 4; i++){
            if(bucket[i] + nums[idx] > length){
                continue;
            }
            bucket[i] += nums[idx];
            if(makeSquare(idx + 1, nums, length, bucket)){
                return true;
            }
            bucket[i] -= nums[idx];
        }
        return false;
    }
    public boolean makesquare(int[] nums) {
        if(nums == null || nums.length < 4){
            return false;
        }
        int sum = 0;
        for(int num : nums){
            sum += num;
        }
        if(sum % 4 != 0){
            return false;
        }
        Arrays.sort(nums);
        reverse(nums);
        int[] bucket = new int[4];
        return makeSquare(0, nums, sum / 4, bucket);
    }
}
```
2. Bit Manipulation  
Goal: Generate four subsets and the sum of each is `length = sum / 4`.  
1)Enumerate all subsets, each sum is `length`.  
2)do `AND` operation between subsets, when they don't have Intersection.Add their `OR` operation result to `okHalf`.  
3)Repeat step 2 on `okHalf` data structure.  
```java
class Solution {
    public boolean makesquare(int[] nums) {
        if(nums == null || nums.length < 4){
            return false;
        }
        int sum = 0;
        for(int num : nums){
            sum += num;
        }
        if(sum % 4 != 0){
            return false;
        }

        int length = sum / 4, n = nums.length;
        int numOfSubsets = 1 << n;
        ArrayList<Integer> okSubset = new ArrayList<>();
        ArrayList<Integer> okHalf = new ArrayList<>();
        //enumerate all subsets which sum equals length
        for(int i = 0; i < numOfSubsets; i++){
            int tmpSum = 0;
            for(int j = 0; j < n; j++){
                //if subset contains nums[j]
                if((i & (1 << j)) != 0){
                    tmpSum += nums[j];
                }
            }
            if(tmpSum == length){
                okSubset.add(i);
            }
        }
        //enumerate half subsets
        for(int i = 0; i < okSubset.size(); i++){
            int set1 = okSubset.get(i);
            for(int j = i + 1; j < okSubset.size(); j++){
                int set2 = okSubset.get(j);
                if((set1 & set2) == 0){
                    okHalf.add((set1 | set2));
                }
            }
        }
        //enumerate all subsets
        for(int i = 0; i < okHalf.size(); i++){
            int set1 = okHalf.get(i);
            for(int j = i + 1; j < okHalf.size(); j++){
                int set2 = okHalf.get(j);
                if((set1 & set2) == 0){
                    return true;
                }
            }
        }
        return false;
    }
}
```
