# 221 Maximal Square – Medium


### Problem:
Given a 2D binary matrix filled with 0’s and 1’s, find the largest square containing all 1’s and return its area.

For example, given the following matrix:
```
1 0 1 0 0
1 0 1 1 1
1 1 1 1 1
1 0 0 1 0
```
Return 4.

### Thoughts:
This is a very obvious dynamic programming problem.

Define a corresponding array, max[i][j], represents the largest square ( only the edge, not the area) using (i, j) as the bottom right corner.

So to calculate max[i][j]

max[i][j] = 0 if matrix[i][j = 0// first row or first column

max[i][j] = 1 if i = 0 or j = 0 and matrix[i][j] = 1// first row or first column

if i != 0 and j != 0 and matrix[i][j] = 1 there are two cases here:

if max[i-1][j] and max[i][j-1] are not the same, then the new largest square is determined by the smaller of these two values,

max[i][j] = smaller + 1

if max[i-1][j] and max[i][j-1] are the same,

the number depends on if matrix[i – max[i-1][j]][j – max[i-1][j]] is 1

if it’s 1 then max[i][j] = max[i-1][j] + 1

if it’s 0 then max[i][j] = max[i-1][j]

Each step in the double loop, check the value of max[i][j], keep a max variable to keep the maximum value so that we could use it to return in the end.

When returning the value, remember to return the square of that because we store the edge length not the actual area in the array.

Better solution is in the improve logic part.
When iterating over an element in the array, if the element is ‘1’, it’s possible to extend an area of ‘1’ with 1 in the side. The condition is that matrix[i-1][j] and matrix[i][j-1] and matrix[i-1][j-1] are all ‘1’.
So we can have the DP equation to be maxs[i][j] = min(maxs[i-1][j-1], maxs[i-1][j], maxs[i][j-1]) + 1 when matrix[i][j] is ‘1’.

### Solutions:

```java
public class Solution {
    public int maximalSquare(char[][] matrix) {
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
            return 0;
        }
        int[][] maxs = new int[matrix.length][matrix[0].length];
        int max = 0;
        for (int i = 0; i < matrix.length; i ++) {
            maxs[i][0] = matrix[i][0] - '0';
            max = Math.max(max, maxs[i][0]);
        }
        for (int j = 0; j < matrix[0].length; j ++) {
            maxs[0][j] = matrix[0][j] - '0';
            max = Math.max(max, maxs[0][j]);
        }
        for (int i = 1; i < matrix.length; i ++) {
            for (int j = 1; j < matrix[0].length; j ++) {
                if (matrix[i][j] == '1') {
                    maxs[i][j] = Math.min(Math.min(maxs[i-1][j-1], maxs[i-1][j]),maxs[i][j-1]) + 1;
                }
                max = Math.max(max, maxs[i][j]);
            }
        }
        return max*max;
    }
}
```