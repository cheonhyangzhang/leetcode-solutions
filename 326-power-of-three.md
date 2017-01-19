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


