# 256. Paint House - Medium

### Problem:
<pre>
There are a row of n houses, each house can be painted with one of the three colors: red, blue or green. The cost of painting each house with a certain color is different. You have to paint all the houses such that no two adjacent houses have the same color.

The cost of painting each house with a certain color is represented by a n x 3 cost matrix. For example, costs[0][0] is the cost of painting house 0 with color red; costs[1][2] is the cost of painting house 1 with color green, and so on... Find the minimum cost to paint all houses.

Note:
All costs are positive integers.
</pre>

### Solutions:

```java
public class Solution {
    public int minCost(int[][] costs) {
        if (costs == null || costs.length == 0 || costs[0].length == 0) {
            return 0;
        }
        int min = Integer.MAX_VALUE;
        int[] c = new int[3];
        int[] newc = new int[3];
        for (int i = 0; i < costs.length; i ++) {
            if (i == 0) {
                c[0] = costs[i][0];
                c[1] = costs[i][1];
                c[2] = costs[i][2];
            }
            else {
                newc[0] = Math.min(c[1], c[2]) + costs[i][0];
                newc[1] = Math.min(c[0], c[2]) + costs[i][1];
                newc[2] = Math.min(c[0], c[1]) + costs[i][2];
                for (int j = 0; j < 3; j ++) {
                    c[j] = newc[j];
                }
            }
            min = Math.min(Math.min(c[0], c[1]), c[2]);
        }
        return min;
    }
}
```