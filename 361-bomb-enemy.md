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