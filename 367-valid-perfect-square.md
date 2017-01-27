# 367 Valid Perfect Square

### Problem:

Given a positive integer num, write a function which returns True if num is a perfect square else False.

Note: Do not use any built-in library function such as sqrt.

Example 1:

```
Input: 16
Returns: True
```
Example 2:
```
Input: 14
Returns: False
```

### Solutions:

```java
public class Solution {
    public boolean isPerfectSquare(int num) {
        for (int i = 0; i * i >= 0 && i * i <= num; i ++) {
            if (i * i == num) {
                return true;
            }
        }
        return false;
    }
}
```

```java
public class Solution {
    public boolean isPerfectSquare(int num) {
        int i = 1;
        while (num > 0) {
            num -= i;
            i += 2;
        }
        return num == 0;
    }
}
```

```java
public class Solution {
    public boolean isPerfectSquare(int num) {
        long left = 0, right = num;
        while (left <= right) {
            long mid = left + (right - left) / 2, t = mid * mid;
            if (t == num) return true;
            else if (t < num) left = mid + 1;
            else right = mid - 1;
        }
        return false;
    }
}
```