# Best Time to Bue and Sell Stock  
## Description  
Say you have an array for which the ith element is the price of a given stock on day i.  
If you were only permitted to complete at most one transaction (ie, buy one and sell one share of the stock), design an algorithm to find the maximum profit.  
## Example  
1.
```
> Input: [7, 1, 5, 3, 6, 4]  
> Output: 5  
> max. difference = 6-1 = 5 (not 7-1 = 6, as selling price needs to be larger than buying price)  
```
2.
```
> Input: [7, 6, 4, 3, 1]  
> Output: 0  
> In this case, no transaction is done, i.e. max profit = 0.  
```
## Solution  
Dynamic Programming.  
dp[i] = max(maxNumber-prices[i], 0)  
Since dp[i] depends only on *prices*,we don't need to new dp array.  
Complexity: Time O(n), Space O(1).  
```java
    public int maxProfit(int[] prices) {
        if(prices.length == 0 || prices == null) return 0;
        int len = prices.length, maxNumber = prices[len - 1], rst = 0, current;
        for(int i = len - 1; i >= 0; i--){
            current = maxNumber - prices[i];
            maxNumber = Math.max(maxNumber, prices[i]);
            rst = Math.max(rst, current);
        }
        return rst;
    }
```
