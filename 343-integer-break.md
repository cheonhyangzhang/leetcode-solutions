# 343 Integer Break

### Problem:

Given a positive integer n, break it into the sum of at least two positive integers and maximize the product of those integers. Return the maximum product you can get.

For example, given n = 2, return 1 (2 = 1 + 1); given n = 10, return 36 (10 = 3 + 3 + 4).

Note: You may assume that n is not less than 2 and not larger than 58.

Hint:

There is a simple O(n) solution to this problem.
You may check the breaking results of n ranging from 7 to 10 to discover the regularities.

### Solutions:

```java
public class Solution {
    public int integerBreak(int n) {
        int[] result = new int[n + 1];
        result[1] = 1;
        for (int i = 2; i <= n; i ++) {
            int max = Integer.MIN_VALUE;
            for (int j = 1; j <= i/2; j ++) {
                int product = Math.max(result[j], j) * Math.max(result[i-j], i - j);
                max = Math.max(max, product);
            }
            result[i] = max;
        }
        return result[n];
    }
}
```

```java
public class Solution {
    public int integerBreak(int n) {
        if (n==2) 
            return 1;
        if (n==3) 
            return 2;
        if (n==4) 
            return 4;
     
        int result=0;
        if ( n % 3 == 0) {
            int m = n/3;
            result = (int) Math.pow(3, m);
        }
        else if( n % 3 == 2){
            int m = n/3;
            result = (int) Math.pow(3, m) * 2;
        }else if( n % 3 == 1){
            int m = (n-4)/3;
            result = (int) Math.pow(3, m) *4;
        }
     
        return result;
    }
}
```

```java
public class Solution {
    public int integerBreak(int n) {
        if (n == 2 || n == 3) 
            return n - 1;
        int res = 1;
        while (n > 4) {
            res *= 3;
            n -= 3;
        }
        return res * n;
    }
}
```

