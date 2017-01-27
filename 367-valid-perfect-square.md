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