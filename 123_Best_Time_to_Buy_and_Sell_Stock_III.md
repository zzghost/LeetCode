# Best Time to Buy and Sell Stock III
Related problems: [121 Best Time to Buy and Sell Stock](https://github.com/zzghost/leetcode/blob/master/121_Best_Time_to_Buy_and_Sell_Stock.md)  
[122 Best Time to Buy and Sell Stock II](https://github.com/zzghost/leetcode/blob/master/122_Best_Time_to_Buy_and_Sell_Stock_II.md)
## Description
Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete at most two transactions.

**Note:**
You may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).

## Solution
Dynamic Programming.  
Two arrays `pre` and `post` to store till the current position the max profit of one transaction, before and after this day respectively.  
`min` and `max` denotes the min and max price.  
`maxprofit` denotes the max profit till the current position.  
The state transition equations are:  
`pre[i] = max{prices[i] - min, maxprofit}`  
`post[i] = max{max - prices[i], maxprofit}`  
`res = max{res, pre[i] + post[i]}`  
**Complexity: Time O(n), space O(n).**
```java
class Solution {
    public int maxProfit(int[] prices) {
        if(prices == null || prices.length == 0)
            return 0;
        int n = prices.length;
        int[] pre = new int[n];
        int[] post = new int[n];
        int min = prices[0], max = prices[n - 1];
        int maxprofit = 0;
        for(int i = 0; i < n; i++){
            int profit = prices[i] - min;
            maxprofit = Math.max(profit, maxprofit);
            min = Math.min(prices[i], min);
            pre[i] = maxprofit;
        }
        maxprofit = 0;
        for(int i = n - 1; i >= 0 ; i--){
            int profit = max - prices[i];
            maxprofit = Math.max(profit, maxprofit);
            max = Math.max(prices[i], max);
            post[i] = maxprofit;
        }
        maxprofit = pre[0] + post[0];
        for(int i = 0; i < n; i++){
            maxprofit = Math.max(maxprofit, pre[i] + post[i]);
        }
        return maxprofit;
    }
}
```
