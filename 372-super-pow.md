# 372 Super Pow

### Problem:

Your task is to calculate ab mod 1337 where a is a positive integer and b is an extremely large positive integer given in the form of an array.

Example1:
```
a = 2
b = [3]

Result: 8
```
Example2:
```
a = 2
b = [1,0]

Result: 1024
```

### Solutions:

```java
public class Solution {
    public int superPow(int a, int[] b) {
        long res = 1;
        a = a % 1337;
        for (int i = 0; i < b.length; ++i) {
            res = pow(res, 10) * pow(a, b[i]) % 1337;
        }
        return (int)res;
    }
    private long pow(long x, int n) {
        if (n == 0) return 1;
        long v = pow(x, n / 2);
        if (n % 2 == 0) {
            return v * v % 1337;
        } 
        else {
            return v * v * x % 1337;
        }
    }
}
```