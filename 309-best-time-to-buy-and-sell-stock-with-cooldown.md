# 309. Best Time to Buy and Sell Stock with Cooldown

### Problem:

<pre>
Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (ie, buy one and sell one share of the stock multiple times) with the following restrictions:

You may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).
After you sell your stock, you cannot buy stock on next day. (ie, cooldown 1 day)
Example:

prices = [1, 2, 3, 0, 2]
maxProfit = 3
transactions = [buy, sell, cooldown, buy, sell]
</pre>

### Solutions:

```java
public class Solution {
    public int maxProfit(int[] prices) {
        if (prices.length == 0) {
            return 0;
        }
        int[] diff = new int[prices.length];
        for (int i = 1; i < prices.length; i ++) {
            diff[i] = prices[i] - prices[i - 1]; 
        }
        int[] in = new int[diff.length];
        int[] out = new int[diff.length];
        for (int i = 1; i < diff.length; i ++) {
            if (i == 1) {
                in[i] = Math.max(diff[i], 0);
                out[i] = 0;
            }
            else {
                in[i] = Math.max(in[i-1], out[i - 2]) + diff[i];
                out[i] = Math.max(in[i-1], out[i-1]);
            }
        }
        return Math.max(in[in.length - 1], out[out.length - 1]);
    }
}
```