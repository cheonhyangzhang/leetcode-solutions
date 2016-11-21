# 64 Minimum Path Sum – Medium

### Problem:



Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right which minimizes the sum of all numbers along its path.

Note: You can only move either down or right at any point in time.


### Thoughts:



This is another modified version of the problem Unique Paths.

Instead of

d[i][j] = d[i-1][j] +d[i][j-1]

Use

d[i][j] = Math.min(d[i-1][j], d[i][j-1]) + nums[i][j]


### Solutions:



```java
public class Solution {
    public int minPathSum(int[][] grid) {
        int m = grid.length;
        int n = grid[0].length;
        int[][] mins = new int[m][n];
        mins[0][0] = grid[0][0];
        for (int i = 1; i < m; i ++){
            mins[i][0] = mins[i-1][0] + grid[i][0];
        }
        for (int j = 1; j < n; j ++){
            mins[0][j] = mins[0][j-1] + grid[0][j];
        }
        for (int i = 1; i < m ; i ++){
            for (int j = 1; j < n; j ++){
                 mins[i][j] = Math.min(mins[i-1][j], mins[i][j-1]) + grid[i][j];
            }
        }
        return mins[m-1][n-1];
    }
}
```