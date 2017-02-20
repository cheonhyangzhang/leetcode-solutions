# 498. Diagonal Traverse

### Problem

Given a matrix of M x N elements (M rows, N columns), return all elements of the matrix in diagonal order as shown in the below image.

Example:
```
Input:
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
Output:  [1,2,4,7,5,3,6,8,9]
Explanation:
```
![](/assets/diagonal_traverse.png)

Note:
1. The total number of elements of the given matrix will not exceed 10,000.

### Solutions:

```java
public class Solution {
    public int[] findDiagonalOrder(int[][] matrix) {
        if (matrix == null || matrix.length == 0) {
            int[] result = new int[0];
            return result;
        }
        int[] result = new int[matrix.length * matrix[0].length];
        int[][] move = new int[2][2];
        move[0] = new int[]{-1, 1};
        move[1] = new int[]{1, -1};
        int dir = 0;
        int i = 0, j = 0;
        for (int k = 0; k < result.length; k ++) {
            result[k] = matrix[i][j];
            i += move[dir][0];
            j += move[dir][1];
            if (i == matrix.length) {
                i = matrix.length - 1;
                j = j + 2;
                dir = dir ^ 1;
            }
            if (j == matrix[0].length) {
                j = matrix[0].length - 1;
                i = i + 2;
                dir = dir ^ 1;
            }
            if (i == -1) {
                i = 0;
                dir = dir ^ 1;
            }
            if (j == -1) {
                j = 0;
                dir = dir ^ 1;
            }
        }
        return result;
    }
}
```

[0,0] -> [0,1], [1,0] -> [2,0],[1,1],[0,2] -> [1,2],[2,1] -> [2,2]
```java
public class Solution {
    public int[] findDiagonalOrder(int[][] matrix) {
        if (matrix == null || matrix.length == 0) {
            int[] result = new int[0];
            return result;
        }
        int[] result = new int[matrix.length * matrix[0].length];
        int m = matrix.length, n = matrix[0].length, k = 0;
        for (int i = 0; i < m + n - 1; ++i) {
            int low = Math.max(0, i - n + 1), high = Math.min(i, m - 1);
            if (i % 2 == 0) {
                for (int j = high; j >= low; --j) {
                    result[k++] = matrix[j][i - j];
                }
            } else {
                for (int j = low; j <= high; ++j) {
                    result[k++] = matrix[j][i - j];
                }
            }
        }
        return result;
    }
}
```