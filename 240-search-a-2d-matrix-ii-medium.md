# 240 Search a 2D Matrix II – Medium

### Problem:
Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:

Integers in each row are sorted in ascending from left to right.
Integers in each column are sorted in ascending from top to bottom.
For example,

Consider the following matrix:
```
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
```
Given target = 5, return true.

Given target = 20, return false.


### Thoughts:

For version one, Search a 2D Matrix, basic idea is to leverage binary search. Since it’s a 2D matrix, then use a 2x binary search can solve the problem.
So for this one, because it’s not the same order as the version I, so we need to check more elements to find the target element if we want to use a 2x binary search.

However, just like the version I, we can do a one binary search by considering the 2D array as 1D array. For this problem, we can notice a property, say for the below example.
```
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
```
In order to find 19, we can start with 18.
* 18 is smaller than 19, because we know all the element in the first column is smaller than 18, so 19 cannot be in the first column, so we move to right, which is 21.
* 21 is bigger than 19, because we know all the element in the same row to the right of 21 is bigger than 21 so 19 cannot be in this row, so we move to up, which is 13.
* Based on the rule above, we go to 14->17->24->22->19.

Also remember to return false, if index is out of bound indicating not found target element.

### Solutions:

```java
public class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        int i = matrix.length - 1;
        int j = 0;
        while (i >= 0 && j < matrix[0].length) {
            if (matrix[i][j] > target) {
                i --;
            }
            else if (matrix[i][j] < target) {
                j ++;
            }
            else {
                return true;
            }
        }
        return false;
    }
}
```