# 361 Bomb Enemy

### Problem:


Given a 2D grid, each cell is either a wall 'W', an enemy 'E' or empty '0' (the number zero), return the maximum enemies you can kill using one bomb.
The bomb kills all the enemies in the same row and column from the planted point until it hits the wall since the wall is too strong to be destroyed.
Note that you can only put the bomb at an empty cell.

Example:
For the given grid
<pre>
0 E 0 0
E 0 W E
0 E 0 0
</pre>


return 3. (Placing a bomb at (1,1) kills 3 enemies)


### Solutions:

```java
public class Solution {
    public int maxKilledEnemies(char[][] grid) {
        int max = 0;
        for (int i = 0; i < grid.length; i ++) {
            for (int j = 0; j < grid[0].length; j ++) {
                if (grid[i][j] != '0') {
                    continue;
                }
                int sum = 0;
                int x = i, y = j;
                while (x >= 0 && grid[x][y] != 'W') {
                    if (grid[x][y] == 'E') {
                        sum ++;
                    }
                    x --;
                }
                x = i; y = j;
                while (x < grid.length && grid[x][y] != 'W') {
                    if (grid[x][y] == 'E') {
                        sum ++;
                    }
                    x ++;
                }
                x = i; y = j;
                while (y >= 0 && grid[x][y] != 'W') {
                    if (grid[x][y] == 'E') {
                        sum ++;
                    }
                    y --;
                }
                x = i; y = j;
                while (y < grid[0].length && grid[x][y] != 'W') {
                    if (grid[x][y] == 'E') {
                        sum ++;
                    }
                    y ++;
                }
                max = Math.max(max, sum);
            }
        }
        return max;
    }
}
```

```java
public class Solution {
    public int maxKilledEnemies(char[][] grid) {
        if (grid == null || grid.length == 0 || grid[0].length == 0) {
            return 0;
        }
        int max = 0;
        int[][] maxs = new int[grid.length][grid[0].length];
        for (int i = 0; i < grid.length; i ++) {
            int sum = 0;
            int start = 0;
            for (int j = 0; j <= grid[0].length; j ++) {
                if (j < grid[0].length && grid[i][j] == 'E') {
                    sum ++;
                }
                else if (j == grid[0].length || grid[i][j] == 'W') {
                    for (int k = start; k < j; k ++) {
                        if (grid[i][k] == 'E') {
                            continue;
                        }
                        maxs[i][k] += sum;
                        max = Math.max(max, maxs[i][k]);
                    }
                    sum = 0;
                    start = j + 1;
                }
            }
        }
        for (int j = 0; j < grid[0].length; j ++) {
            int sum = 0;
            int start = 0;
            for (int i = 0; i <= grid.length; i ++) {
                if (i < grid.length && grid[i][j] == 'E') {
                    sum ++;
                }
                else if (i == grid.length || grid[i][j] == 'W' ) {
                    for (int k = start; k < i; k ++) {
                        if (grid[k][j] == 'E') {
                            continue;
                        }
                        maxs[k][j] += sum;
                        max = Math.max(max, maxs[k][j]);
                    }
                    sum = 0;
                    start = i + 1;
                }
            }
        }
        return max;
    }
}
```

```java
public class Solution {
    public int maxKilledEnemies(char[][] grid) {
        int m = grid.length;
        int n = m > 0 ? grid[0].length : 0;

        int result = 0, rows = 0;
        int[] cols = new int[n];
        for (int i = 0; i < m; ++i) {
            for (int j = 0; j < n; ++j) {
                if (j == 0 || grid[i][j-1] == 'W') {
                    rows = 0;
                    for (int k = j; k < n && grid[i][k] != 'W'; ++k)
                        if (grid[i][k] == 'E')
                            rows += 1;
                }
                if (i == 0 || grid[i-1][j] == 'W') {
                    cols[j] = 0;
                    for (int k = i; k < m && grid[k][j] != 'W'; ++k)
                        if (grid[k][j] == 'E')
                            cols[j] += 1;
                }

                if (grid[i][j] == '0' && rows + cols[j] > result)
                    result = rows + cols[j];
            }
        }
        return result;
    }
}
```