# 62 Unique Paths II – Medium


### Problem:



Follow up for “Unique Paths”:

Now consider if some obstacles are added to the grids. How many unique paths would there be?

An obstacle and empty space is marked as 1 and 0 respectively in the grid.

For example,

There is one obstacle in the middle of a 3×3 grid as illustrated below.

[
  [0,0,0],
  [0,1,0],
  [0,0,0]
]
The total number of unique paths is 2.

Note: m and n will be at most 100.


### Thoughts:



This problem is almost identical to Unique Paths problem. The only difference is that there are conditions when assigning value to d[i][j].

d[i][j] = 0 if board[i][j] == 1

d[i][j] = d[i-1][j] +d[i][j-1] othwerwise

Plus, now d[i][0] and d[0][j] is not sure to be 1.

### Solutions:



```java
public class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        int m = obstacleGrid.length;
        int n = obstacleGrid[0].length;
        int[][] paths = new int[m][n];
        if (obstacleGrid[0][0] == 0){
            paths[0][0] = 1;
        }
        else{
            paths[0][0] = 0;
        }
        for (int i = 1; i < m; i ++){
            if (obstacleGrid[i][0] == 0 && paths[i-1][0] == 1){
                paths[i][0] = 1;
            }
            else{
                paths[i][0] = 0;
            }
        }
        for (int j = 1; j < n; j ++){
            if (obstacleGrid[0][j] == 0 && paths[0][j-1] == 1){
                paths[0][j] = 1;
            }
            else{
                paths[0][j] = 0;
            }
        }
        for (int i = 1; i < m ; i ++){
            for (int j = 1; j < n; j ++){
                if (obstacleGrid[i][j] == 1){
                    paths[i][j] = 0;
                }
                else{
                    paths[i][j] = paths[i-1][j] + paths[i][j-1];
                }
            }
        }
        return paths[m-1][n-1];
    }
}
```