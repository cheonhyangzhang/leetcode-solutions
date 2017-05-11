# 200 Number of Islands – Medium

### Problem:
Given a 2d grid map of '1's (land) and '0's (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

Example 1:
```
11110
11010
11000
00000
```
Answer: 1

Example 2:
```
11000
11000
00100
00011
```
Answer: 3

### Thoughts:
This is very typical DFS problem. For each unvisited “1”, spread to mark all “1” in the same island visited. Then find next unvisited “1”, repeat the same thing.

One thing to differentiate BFS and DFS is that BFS only iterates inside of a connected graph while DFS visit all nodes, it works for a forrest.

In this problem, it is like find all trees in a forrest. How many trees exist in a forrest.

Based on original standard DFS, 0 is white, 1 is gray and 2 is black
Actually for this problem boolean for visited matrix is already good enough. The solution below is just to follow the idea of DFS, which is not very necessary for this problem.

### Solutions:

```java
public class Solution {
    public int numIslands(char[][] grid) {
        if (grid.length == 0 || grid[0].length == 0) {
            return 0;
        }
        int m = grid.length, n = grid[0].length;
        int count = 0;
        for (int i = 0; i < m ; i ++) {
            for (int j = 0; j < n; j ++) {
                if (grid[i][j] == '1') {
                    count ++;
                    dfs(grid, m, n, i, j);
                }
            }
        }
        return count;
    }
    private void dfs(char[][] grid, int m, int n, int i, int j) {
        if (i < 0 || i >= m || j < 0 || j >= n || grid[i][j] != '1') {
            return;
        }
        grid[i][j] = 'X';
        dfs(grid, m, n, i - 1, j);
        dfs(grid, m, n, i + 1, j);
        dfs(grid, m, n, i, j - 1);
        dfs(grid, m, n, i, j + 1);
    }
}
```