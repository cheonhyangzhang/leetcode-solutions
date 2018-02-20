# 74 Search a 2D Matrix – Medium


### Problem:



Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:

Integers in each row are sorted from left to right.
The first integer of each row is greater than the last integer of the previous row.
For example,

Consider the following matrix:

[
  [1,   3,  5,  7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
]
Given target = 3, return true.


### Thoughts:



O(n^2) would be the straight forward way, iterating over every single number in the matrix.

However, a better solution is using two-times binary search which will improve running time to logm + logn.

2x Binary search using BS to find the correct row first, then inside of a give row, using BS for the second time to find the target.

However, according to LeetCode’s checking condition, this approach is having

java.lang.StackOverflowError

Probably it doesn’t like Recursion version for the solution. It has this error even for test case [[1],[3]] with target of 2.

So working approach to pass is do a 2D version of BS, this approach has log(m*n) running time.

It’s lgm + lgn vs log(m*n).


### Solutions:

Simplified version which is one binary search, actually this is log(m*n) but since log(m*n) = log(m) + log(n), so the time complexity is the same as above solution.

```java
public class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        if (matrix == null || matrix.length == 0 || matrix[0] == null || matrix[0].length == 0) {
            return false;
        }
        int m = matrix.length, n = matrix[0].length;
        int start = 0, end = m*n -1;
        while (start <= end) {
            int mid = (start + end) / 2;
            int tmp = matrix[mid/n][mid%n];
            if (tmp > target) {
                end = mid - 1;
                continue;
            }
            if (tmp < target) {
                start = mid + 1;
                continue;
            }
            return true;
        }
        return false;
    }
}
```