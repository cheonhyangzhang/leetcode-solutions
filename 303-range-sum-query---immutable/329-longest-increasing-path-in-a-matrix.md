# 329 Longest Increasing Path in a Matrix

### Problem:
Given an integer matrix, find the length of the longest increasing path.

From each cell, you can either move to four directions: left, right, up or down. You may NOT move diagonally or move outside of the boundary (i.e. wrap-around is not allowed).

Example 1:
```
nums = [
  [9,9,4],
  [6,6,8],
  [2,1,1]
]
```
Return 4
The longest increasing path is [1, 2, 6, 9].
Example 2:
```
nums = [
  [3,4,5],
  [3,2,6],
  [2,2,1]
]
```
Return 4
The longest increasing path is [3, 4, 5, 6]. Moving diagonally is not allowed.

# Solutions:

```java
public class Solution {
    public int longestIncreasingPath(int[][] matrix) {
        if( matrix == null || matrix.length==0 || matrix[0].length == 0) {
            return 0;
        }
        int[] dx = {0, 1, 0, -1};
        int[] dy = {1, 0, -1, 0};
        int[][] maxs = new int[matrix.length][matrix[0].length];
        int max = 0;
        for(int i = 0; i < matrix.length; i++){
            for(int j = 0; j < matrix[0].length; j++){
                max = Math.max(max, dfs(dx, dy, matrix, i, j, maxs));
            }
        }
        return max;
    }
 
    public int dfs(int[] dx, int[] dy, int[][] matrix, int i, int j,  int[][] maxs){
        if(maxs[i][j] != 0) {
            return maxs[i][j];
        }
        for(int m = 0; m < 4; m++){
            int x = i + dx[m];
            int y = j + dy[m];
 
            if(x >= 0 && y >= 0 && x < matrix.length && y < matrix[0].length && matrix[x][y]>matrix[i][j]){
                maxs[i][j] = Math.max(maxs[i][j], dfs(dx, dy, matrix, x, y, maxs));
            }
        } 
        maxs[i][j] ++;
        return maxs[i][j];
    }
}
```