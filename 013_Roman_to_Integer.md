# Roman to Integer
Given a roman numeral, convert it to an integer.

Input is guaranteed to be within the range from 1 to 3999.
## Solution
```java
class Solution {
    public int romanToInt(String s) {
        int[] nums = new int[s.length()];
        for(int i = 0; i < s.length(); i++){
            switch(s.charAt(i)){
            //Ⅰ（1）、X（10）、C（100）、M（1000）、V（5）、L（50）、D（500）
                case 'I': nums[i] = 1;break;
                case 'X': nums[i] = 10;break;
                case 'C': nums[i] = 100;break;
                case 'M': nums[i] = 1000;break;
                case 'V': nums[i] = 5;break;
                case 'L': nums[i] = 50;break;
                case 'D': nums[i] = 500;break;
            }
        }
        int sum = 0;
        for(int i = 0; i < nums.length - 1; i++){
            if(nums[i] < nums[i + 1])
                sum -= nums[i];
            else
                sum += nums[i];
        }
        return sum + nums[nums.length - 1];
    }
}
```
