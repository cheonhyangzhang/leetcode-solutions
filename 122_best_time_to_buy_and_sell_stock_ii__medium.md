# 122 Best Time to Buy and Sell Stock II – Medium


### Problem:



Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (ie, buy one and sell one share of the stock multiple times). However, you may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).


### Thoughts:



This seems to be tricky but after calculating the diff between days, it becomes a problem to calculate the sum of non-negative elements in an array.


### Solutions:


```java
public class Solution {
    public int maxProfit(int[] prices) {
        int p = 0;
        for (int i = 1; i < prices.length; i ++) {
            p += Math.max(0, prices[i] - prices[i-1]);
        }
        return p;
    }
}
```