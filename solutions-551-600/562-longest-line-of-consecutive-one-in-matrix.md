# 562 Longest Line of Consecutive One in Matrix

### Problem:

Given a 01 matrix M, find the longest line of consecutive one in the matrix. The line could be horizontal, vertical, diagonal or anti-diagonal.

Example:
```
Input:
[[0,1,1,0],
 [0,1,1,0],
 [0,0,0,1]]
Output: 3
```

Hint: The number of elements in the given matrix will not exceed 10,000.

### Solutions:

```java
public class Solution {
    public int longestLine(int[][] M) {
        int res = 0;
        if (M == null || M.length == 0 || M[0].length == 0) {
            return 0;
        }
        int m = M.length, n = M[0].length;
        int[][][] dp = new int[m][n][4];
        // dp[x][y][0] is for horizontal
        // dp[x][y][1] is for vertical
        // dp[x][y][2] is for diagonal
        // dp[x][y][3] is for anti-diagonal
        dp[0][0][0] = dp[0][0][1] = dp[0][0][2] = M[0][0];
        dp[0][n - 1][3] = M[0][n - 1];
        res = Math.max(res, M[0][0]);
        for (int i = 1; i < m; i ++) {
            if (M[i][0] == 1) {
                dp[i][0][0] = 1;
                dp[i][0][1] = dp[i - 1][0][1] + 1;
                dp[i][0][2] = 1;
                res = Math.max(res, dp[i][0][1]);
            }
            if (M[i][n - 1] == 1) {
                dp[i][n - 1][3] = 1;
                res = Math.max(res, 1);
            }
        }
        for (int j = 1; j < n; j ++) {
            if (M[0][j] == 1) {
                dp[0][j][0] = dp[0][j - 1][0] + 1;
                dp[0][j][1] = 1;
                dp[0][j][2] = 1;
                dp[0][j][3] = 1;
                res = Math.max(res, dp[0][j][0]);
            }
        }
        for (int i = 0; i < m; i ++) {
            for (int j = 0; j < n; j ++) {
                if (M[i][j] == 1) {
                    if (j > 0) {
                        dp[i][j][0] = dp[i][j - 1][0] + 1;
                    }
                    if (i > 0) {
                        dp[i][j][1] = dp[i - 1][j][1] + 1;
                    }
                    if (i > 0 && j > 0) {
                        dp[i][j][2] = dp[i - 1][j - 1][2] + 1;
                    }
                    if (j < n - 1 && i > 0) {
                        dp[i][j][3] = dp[i - 1][j + 1][3] + 1;
                    }
                    res = Math.max(res, dp[i][j][0]);
                    res = Math.max(res, dp[i][j][1]);
                    res = Math.max(res, dp[i][j][2]);
                    res = Math.max(res, dp[i][j][3]);
                }
            }
        }
        return res;
    }
}
```