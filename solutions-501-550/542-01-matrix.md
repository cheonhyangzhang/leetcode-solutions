# 542. 01 Matrix

### Problem:
Given a matrix consists of 0 and 1, find the distance of the nearest 0 for each cell.

The distance between two adjacent cells is 1.
Example 1: 
Input:
```
0 0 0
0 1 0
0 0 0
```
Output:
```
0 0 0
0 1 0
0 0 0
```
Example 2: 
Input:
```
0 0 0
0 1 0
1 1 1
```
Output:
```
0 0 0
0 1 0
1 2 1
```

Note:
1. The number of elements of the given matrix will not exceed 10,000.
2. There are at least one 0 in the given matrix.
3. The cells are adjacent in only four directions: up, down, left and right.

### Solutions:

```java
public class Solution {
    public int[][] updateMatrix(int[][] matrix) {
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
            return matrix;
        }
        int[][] dirs = new int[][]{{-1, 0}, {1, 0}, {0, -1}, {0, 1}};
        Queue<Integer> qx = new LinkedList<Integer>();
        Queue<Integer> qy = new LinkedList<Integer>();
        for (int i = 0; i < matrix.length; i ++) {
            for (int j = 0; j < matrix[0].length; j ++) {
                if (matrix[i][j] == 0) {
                    qx.add(i);
                    qy.add(j);
                }
                else {
                    matrix[i][j] = Integer.MAX_VALUE;
                }
            }
        }
        while (!qx.isEmpty()) {
            int x = qx.poll();
            int y = qy.poll();
            for (int i = 0; i < dirs.length; i ++) {
                int nx = x + dirs[i][0];
                int ny = y + dirs[i][1];
                if (nx >= 0 && nx < matrix.length && ny >= 0 && ny < matrix[0].length && matrix[nx][ny] > matrix[x][y] + 1) {
                    matrix[nx][ny] = matrix[x][y] + 1;
                    qx.add(nx);
                    qy.add(ny);
                }
            }
        }
        return matrix;
    }
}
```