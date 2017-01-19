# 326 Power of Three

### Problem:

Given an integer, write a function to determine if it is a power of three.

Follow up:
Could you do it without using any loop / recursion?

### Solutions:

```java
public class Solution {
    public boolean isPowerOfThree(int n) {
        if (n <= 0) {
            return false;
        }
        while (n > 1) {
            if (n % 3 != 0) {
                return false;
            }
            n = n / 3;
        }
        return true;
    }
}
```

```java
public class Solution {
    public boolean isPowerOfThree(int n) {
        return n>0?(1162261467 % n) == 0:false;  
    }
}
```

```java
public class Solution {
    public boolean isPowerOfThree(int n) {
         return (n == 1 || n == 3 || n == 9 || n == 27 || n == 81 || n == 243 || n == 729 || n == 2187 || n == 6561 || n == 19683 || n == 59049 || n == 177147 || n == 531441 || n == 1594323 || n == 4782969 || n == 14348907 || n == 43046721 || n == 129140163 || n == 387420489 || n == 1162261467);  
    }
}
```

```java
public class Solution {
    public boolean isPowerOfThree(int n) {
        double res = Math.log10(n) / Math.log10(3);  
        return Double.compare(res, (int)res) == 0;
    }
}
```




