# 48 Rotate Image – Medium


### Problem:



You are given an n x n 2D matrix representing an image.

Rotate the image by 90 degrees (clockwise).

Follow up:
Could you do this in-place?


### Thoughts:



This is only a problem about writing formula.


### Solutions:



```java
public class Solution {
    public void rotate(int[][] matrix) {
        int n = matrix.length;
        for (int i = 0; i < n / 2; i++) {
            for (int j = 0; j < Math.ceil(((double) n) / 2.); j++) {
                int temp = matrix[i][j];
                matrix[i][j] = matrix[n-1-j][i];
                matrix[n-1-j][i] = matrix[n-1-i][n-1-j];
                matrix[n-1-i][n-1-j] = matrix[j][n-1-i];
                matrix[j][n-1-i] = temp;
            }
        }
    }
}
```
Alternative solution:

```java
public class Solution {
    public void rotate(int[][] matrix) {
        if (matrix.length < 2) {
            return;
        }
        int n = matrix.length, m = matrix[0].length;
        for (int i = 0; i < (n + 1)/2; i ++) {
            for (int j = 0; j < m/2; j ++) {
                int tmp = matrix[i][j];
                matrix[i][j] = matrix[n- j - 1][i];
                matrix[n- j - 1][i] = matrix[n - i - 1][m - j - 1];
                matrix[n - i - 1][m - j - 1] = matrix[j][m - i - 1];
                matrix[j][m - i - 1] = tmp;
            }
        }
    }
}
```