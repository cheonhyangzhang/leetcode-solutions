# 417 Pacific Atlantic Water Flow

### Problem:

Given an m x n matrix of non-negative integers representing the height of each unit cell in a continent, the "Pacific ocean" touches the left and top edges of the matrix and the "Atlantic ocean" touches the right and bottom edges.

Water can only flow in four directions (up, down, left, or right) from a cell to another one with height equal or lower.

Find the list of grid coordinates where water can flow to both the Pacific and Atlantic ocean.

Note:
The order of returned grid coordinates does not matter.
Both m and n are less than 150.
Example:
```
Given the following 5x5 matrix:

  Pacific ~   ~   ~   ~   ~ 
       ~  1   2   2   3  (5) *
       ~  3   2   3  (4) (4) *
       ~  2   4  (5)  3   1  *
       ~ (6) (7)  1   4   5  *
       ~ (5)  1   1   2   4  *
          *   *   *   *   * Atlantic

Return:

[[0, 4], [1, 3], [1, 4], [2, 2], [3, 0], [3, 1], [4, 0]] (positions with parentheses in above matrix).
Show Company Tags
Show Tags

```

### Solutions:

```java
public class Solution {
    private class Land {
        private int x;
        private int y;
        public Land(int x, int y) {
            this.x = x;
            this.y = y;
        }
    }
    public List<int[]> pacificAtlantic(int[][] matrix) {
        List<int[]> result = new LinkedList<int[]>();
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
            return result;
        }
        boolean[][] pa = new boolean[matrix.length][matrix[0].length];
        boolean[][] at = new boolean[matrix.length][matrix[0].length];
        Queue<Land> paq = new LinkedList<Land>();
        Queue<Land> atq = new LinkedList<Land>();
        for (int i = 0; i < matrix.length; i ++) {
            pa[i][0] = true;
            at[i][matrix[0].length - 1] = true;
            paq.add(new Land(i, 0));
            atq.add(new Land(i, matrix[0].length - 1));
        }
        for (int j = 0; j < matrix[0].length; j ++) {
            pa[0][j] = true;
            at[matrix.length - 1][j] = true;
            paq.add(new Land(0, j));
            atq.add(new Land(matrix.length - 1, j));
        }
        while (!paq.isEmpty()) {
            Land l = paq.poll();
            int x = l.x, y = l.y;
            process(matrix[x][y], x - 1, y, pa, paq, matrix);
            process(matrix[x][y], x, y - 1, pa, paq, matrix);
            process(matrix[x][y], x + 1, y, pa, paq, matrix);
            process(matrix[x][y], x, y + 1, pa, paq, matrix);
        }
        while (!atq.isEmpty()) {
            Land l = atq.poll();
            int x = l.x, y = l.y;
            process(matrix[x][y], x - 1, y, at, atq, matrix);
            process(matrix[x][y], x, y - 1, at, atq, matrix);
            process(matrix[x][y], x + 1, y, at, atq, matrix);
            process(matrix[x][y], x, y + 1, at, atq, matrix);
        }
        for (int i = 0; i < matrix.length; i ++) {
            for (int j = 0; j < matrix[0].length; j ++) {
                if (pa[i][j] && at[i][j]) {
                    result.add(new int[]{i, j});
                }
            }
        }
        return result;
    }
    private void process(int before, int x, int y, boolean[][] data, Queue<Land> q, int[][] matrix) {
        if (x < 0 || y < 0 || x >= data.length || y >= data[0].length || data[x][y] == true) {
            return;
        }
        if (matrix[x][y] < before) {
            return;
        }
        q.add(new Land(x, y));
        data[x][y] = true;
    }
}
```

```java

```