# 50 Pow(x, n) – Medium


### Problem:



Implement pow(x, n).


### Thoughts:



The most straight forward way it to multiply x n times, but this approach will end up with O(n) time.

It could be faster to be O(lgn) using divide and conquer.


### Solutions:

Note:
-Integer.MIN_VALUE = Integer.MIN_VALUE

```java
public class Solution {
    public double myPow(double x, int n) {
        if (n < 0) {
            return 1 / power(x, -n);
        } 
        else {
            return power(x, n);
        }
    }//myPow
    public double power(double x, int n) {
        if (n == 0)
            return 1;
        double v = power(x, n / 2);
        if (n % 2 == 0) {
            return v * v;
        } 
        else {
            return v * v * x;
        }
    }//power
}
```

```java
class Solution {
    public double myPow(double x, int n) {
        return pow(x, n);
    }
    private double pow(double x, long n) {
        if (n == 0) {
            return 1;
        }
        if (n < 0) {
            return 1 / pow(x, -n);
        }
        double v = pow(x, n / 2);
        if (n % 2 == 0) {
            return v*v;
        }
        else {
            return v*v*x;
        }
    }
}
```