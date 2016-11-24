# 123 Best Time to Buy and Sell Stock III – Hard


### Problem:


Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete at most two transactions.

Note:
You may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).

### Thoughts:


We will need to divide this problem into two subproblem. We find the max profit for range 0..i and i + 1..n -1, then we add up the two max profit we will get the expected result.

### Solutions:

```java
public class Solution {
    public int maxProfit(int[] prices) {
        int[] first = new int[prices.length];
        //first[i] is the max profit for the range 0 .. i, 
        int minPrice = Integer.MAX_VALUE;
        int max = 0;
        for (int i = 0; i < prices.length; i ++) {
            minPrice = Math.min(minPrice, prices[i]);
            max = Math.max(max, prices[i] - minPrice);
            first[i] =  max;
        }
        int maxPrice = Integer.MIN_VALUE;
        max = 0;
        for (int i = prices.length - 1; i > 0; i --) {
            maxPrice = Math.max(maxPrice, prices[i]);
            max = Math.max(max, maxPrice - prices[i] + first[i-1]);
        }
        if (prices.length > 0) {
            max = Math.max(max, first[first.length - 1]);
        }
        return max;
    }
}
```

