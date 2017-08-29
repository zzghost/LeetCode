# Best Time to Buy and Sell Stock II
## Description  
Say you have an array for which the ith element is the price of a given stock on day i.  
Design an algorithm to find the maximum profit. You may complete as many transactions as you like (ie, buy one and sell one share of the stock multiple times). However, you may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).  
## Solution  
Dynamic Programming.  
This problem is same as `121, Best time to buy and sell stcok`.However it allows multiple transactions.  
dp[i] = max(maxProfit + prices[i+1] - prices[i], maxNum - prices[i]).  
1st item: maxProfit is the return value. This item calculates the difference.  
2nd item: maxNum is the so-far max value. This item calculates just 2 numbers' difference.  
Complexity:Time O(n), Space O(1).  
```java
public int maxProfit(int[] prices) {
    if(prices == null || prices.length == 0) return 0;
    int len = prices.length;
    int maxNum = prices[len - 1];
    int maxProfit = 0;
    for(int i = len - 2; i >= 0; i--){
        int curr = Math.max(maxProfit + prices[i+1] - prices[i], maxNum - prices[i]);
        maxProfit = Math.max(curr, maxProfit);
        maxNum = Math.max(maxNum, prices[i]);
    }
    return maxProfit;
}
```
