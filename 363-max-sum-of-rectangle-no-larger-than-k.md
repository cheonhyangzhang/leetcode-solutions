# 363. Max Sum of Rectangle No Larger Than K

### Problem:

Given a non-empty 2D matrix matrix and an integer k, find the max sum of a rectangle in the matrix such that its sum is no larger than k.

Example:
```
Given matrix = [
  [1,  0, 1],
  [0, -2, 3]
]
k = 2
```
The answer is 2. Because the sum of rectangle [[0, 1], [-2, 3]] is 2 and 2 is the max number no larger than k (k = 2).

Note:
1. The rectangle inside the matrix must have an area > 0.
2. What if the number of rows is much larger than the number of columns?

### Solutions:

```java
public class Solution {
    public int maxSumSubmatrix(int[][] matrix, int k) {
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
            return 0;
        }
        int[][] maxs = new int[matrix.length][matrix[0].length];
        
        init(maxs, matrix, k);
        for (int i = 1; i < matrix.length; i ++) {
            for (int j = 1; j < matrix[0].length; j ++) {
                maxs[i][j] = maxs[i - 1][j] + maxs[i][j - 1] - maxs[i - 1][j - 1] + matrix[i][j];
            }
        }
        int max = Integer.MIN_VALUE;
        for (int i = 0; i < maxs.length; i ++) {
            for (int j = 0; j < maxs[0].length; j ++) {
                for (int m = i; m < maxs.length; m ++) {
                    for (int n = j; n < maxs[0].length; n ++) {
                        int tmp = maxs[m][n];
                        if (i - 1 >= 0) {
                            tmp -= maxs[i - 1][n];
                        }
                        if (j - 1 >= 0) {
                            tmp -= maxs[m][j - 1];
                        }
                        if (i - 1 >= 0 && j - 1 >= 0) {
                            tmp += maxs[i - 1][j - 1];
                        }
                        if (tmp <= k) {
                            max = Math.max(max, tmp);
                        }
                    }
                }
            }
        }
        return max;
    }
    private void init(int[][] maxs, int[][] matrix, int k) {
        for (int i = 0; i < matrix.length; i ++) {
            if (i == 0) {
                maxs[i][0] = matrix[i][0];
            }
            else {
                maxs[i][0] = maxs[i - 1][0] + matrix[i][0];
            }
        }
        for (int j = 0; j < matrix[0].length; j ++) {
            if (j == 0) {
                maxs[0][j] = matrix[0][j];
            }
            else {
                maxs[0][j] = maxs[0][j - 1] + matrix[0][j];
            }
        }
    }
}
```

### Solutions:

```java
public class Solution {
    public int maxSumSubmatrix(int[][] matrix, int k) {
        if(matrix==null||matrix.length==0||matrix[0].length==0)
            return 0;
     
        int m=matrix.length;
        int n=matrix[0].length;
     
        int result = Integer.MIN_VALUE;
     
        for(int c1=0; c1<n; c1++){
            int[] each = new int[m];
            for(int c2=c1; c2>=0; c2--){
     
                for(int r=0; r<m; r++){
                    each[r]+=matrix[r][c2];   
                }
     
                result = Math.max(result, getLargestSumCloseToK(each, k));
            }
        }
     
        return result;
    }
     
    public int getLargestSumCloseToK(int[] arr, int k){
        int sum=0;
        TreeSet<Integer> set = new TreeSet<Integer>();
        int result=Integer.MIN_VALUE;
        set.add(0);
     
        for(int i=0; i<arr.length; i++){
            sum=sum+arr[i];
     
            Integer ceiling = set.ceiling(sum-k);
            if(ceiling!=null){
                result = Math.max(result, sum-ceiling);        
            }
     
            set.add(sum);
        }
     
        return result;
    }
}
```