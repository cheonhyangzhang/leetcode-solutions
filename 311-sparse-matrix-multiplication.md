# 311 Sparse Matrix Multiplication

### Problem:

<pre>
Given two sparse matrices A and B, return the result of AB.

You may assume that A's column number is equal to B's row number.

Example:

A = [
  [ 1, 0, 0],
  [-1, 0, 3]
]

B = [
  [ 7, 0, 0 ],
  [ 0, 0, 0 ],
  [ 0, 0, 1 ]
]


     |  1 0 0 |   | 7 0 0 |   |  7 0 0 |
AB = | -1 0 3 | x | 0 0 0 | = | -7 0 3 |
                  | 0 0 1 |
            
</pre>

### Solutions:

```java
public class Solution {
    public int[][] multiply(int[][] A, int[][] B) {
        int m = A.length, k = A[0].length, n = B[0].length;
        int[][] result = new int[m][n];
        for (int i = 0; i < m; i ++) {
            for (int j = 0; j < n; j ++) {
                int sum = 0;
                for (int l = 0; l < k; l ++) {
                    sum +=A[i][l] * B[l][j];
                }
                result[i][j] = sum;
            }
        }
        return result;
    }
}
```

```java
public class Solution {
    public int[][] multiply(int[][] A, int[][] B) {
        int m = A.length, k = A[0].length, n = B[0].length;
        int[][] result = new int[m][n];
        for (int i = 0; i < m; i ++) {
            for (int l = 0; l < k; l ++) {
                if (A[i][l] != 0) {
                    for (int j = 0; j < n; j ++) {
                        result[i][j] +=A[i][l] * B[l][j];
                    }
                }
            }
        }
        return result;
    }
}
```