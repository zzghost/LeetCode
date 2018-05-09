# Largest Number
DescriptionHintsSubmissionsDiscussSolution
Given a list of non negative integers, arrange them such that they form the largest number.

Example 1:
```
Input: [10,2]
Output: "210"
```
Example 2:
```
Input: [3,30,34,5,9]
Output: "9534330"
```
**Note:** The result may be very large, so you need to return a string instead of an integer.
## Solution
```java
class Solution {
    class MyComparator implements Comparator{
        @Override
        public int compare(Object o1, Object o2){
            String s1 = (String)o1;
            String s2 = (String)o2;
            return (s2 + s1).compareTo(s1 + s2);
        }
    }
    public String largestNumber(int[] nums) {
        ArrayList<String> numbers = new ArrayList<>();
        for(int num : nums){
            numbers.add(String.valueOf(num));
        }
        MyComparator mc = new MyComparator();
        Collections.sort(numbers, mc);
        StringBuilder sb = new StringBuilder();
        for(String str : numbers){
            sb.append(str);
        }
        String rst = sb.toString();
        if(rst.indexOf("0") == 0){
            return "0";
        }
        return rst;
    }
}
```
