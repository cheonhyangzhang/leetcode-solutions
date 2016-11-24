# 121 Best Time to Buy and Sell Stock – Medium


### Problem:



Say you have an array for which the ith element is the price of a given stock on day i.

If you were only permitted to complete at most one transaction (ie, buy one and sell one share of the stock), design an algorithm to find the maximum profit.


### Thoughts:



Very straight forward. Using a variable to keep the current min value, then max candidate is current value – current min value.


### Solutions:


```java
public class Solution {
    public int maxProfit(int[] prices) {
        if (prices == null || prices.length == 0) {
            return 0;
        }
        int minPrice = prices[0];
        int max = 0;
        for (int i = 1; i < prices.length; i ++) {
            max = Math.max(max, prices[i] - minPrice);
            minPrice = Math.min(minPrice, prices[i]);
        }
        return max;
    }
}
```