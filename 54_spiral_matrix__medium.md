# 54 Spiral Matrix – Medium


### Problem:



Given a matrix of m x n elements (m rows, n columns), return all elements of the matrix in spiral order.

For example,
Given the following matrix:

[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
You should return [1,2,3,6,9,8,7,4,5].


### Thoughts:


Go in a Spiral Way, one trip contains four part, go right, go down, go left and go up.

Repeat Spiral trip until there is only one column or row left.


### Solutions:


```java
public class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        List<Integer> result = new ArrayList<Integer>();
        if(matrix == null || matrix.length == 0) return result;
        int m = matrix.length;
        int n = matrix[0].length;
        int x=0;
        int y=0;
        while(m>0 && n>0){
        //if one row/column left, no circle can be formed
            if(m==1){
                for(int i=0; i<n; i++){
                    result.add(matrix[x][y++]);
                }
                break;
            }
            else if(n==1){
                for(int i=0; i<m; i++){
                    result.add(matrix[x++][y]);
                }
                break;
            }
            //below, process a circle
            //top - move right
            for(int i=0;i<n-1;i++){
                result.add(matrix[x][y++]);
            }
            //right - move down
            for(int i=0;i<m-1;i++){
                result.add(matrix[x++][y]);
            }
            //bottom - move left
            for(int i=0;i<n-1;i++){
                result.add(matrix[x][y--]);
            }
            //left - move up
            for(int i=0;i<m-1;i++){
                result.add(matrix[x--][y]);
            }
            x++;
            y++;
            m=m-2;
            n=n-2;
        }
        return result;
    }
}
```
Alternative solution:

```java
public class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
       List<Integer> result = new LinkedList<Integer>();
       if (matrix.length == 0) {
           return result;
       }
       int left = 0, right = matrix[0].length - 1, up = 0, down = matrix.length - 1;
       int i = 0, j = 0, deltaI = 0, deltaJ = 1;
       while (left <= right && up <=down) {
           if (j > right) {
               deltaJ = 0;
               deltaI = 1;
               j = right;
               up ++;
           }
           else if (i > down) {
               deltaJ = -1;
               deltaI = 0;
               i = down;
               right --;
           }
           else if (j < left) {
               deltaJ = 0;
               deltaI = -1;
               j = left;
               down --;
           }
           else if (i < up) {
               deltaI = 0;
               deltaJ = 1;
               i = up;
               left ++;
           }
           else {
               result.add(matrix[i][j]);
           }
           i = i + deltaI;
           j = j + deltaJ;
       }
       return result;
    }
     
}
```