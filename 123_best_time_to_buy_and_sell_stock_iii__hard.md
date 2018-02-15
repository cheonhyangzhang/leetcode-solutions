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

```java
class Solution {
    public int maxProfit(int[] prices) {
        int[][][] dp = new int[prices.length+1][3][2];
        int res = 0;
        dp[0][0][0] = dp[0][1][0] = dp[0][2][0] = 0 ;
        dp[0][0][1] = dp[0][1][1] = dp[0][2][1] = Integer.MIN_VALUE;
        
        for (int i = 1; i <= prices.length; i ++) {
            dp[i][0][0] = 0;
            dp[i][0][1] = Integer.MIN_VALUE;
            dp[i][1][0] = Math.max(dp[i-1][1][0], dp[i-1][1][1] + prices[i-1]);
            dp[i][1][1] = Math.max(dp[i-1][1][1], dp[i-1][0][0] - prices[i-1]);
            dp[i][2][0] = Math.max(dp[i-1][2][0], dp[i-1][2][1] + prices[i-1]);
            dp[i][2][1] = Math.max(dp[i-1][2][1], dp[i-1][1][0] - prices[i-1]);
            System.out.println(dp[i][1][0] +", " + dp[i][1][1] + ", " + dp[i][2][0] + ", " + dp[i][2][1]);
            for (int j = 0; j < 3; j ++) {
                for (int k = 0; k < 2; k ++) {
                    res = Math.max(res, dp[i][j][k]);
                }
            }
        }
        return res;
    }
}
```

