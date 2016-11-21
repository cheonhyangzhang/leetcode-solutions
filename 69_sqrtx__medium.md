# 69 Sqrt(x) – Medium


### Problem:



Implement int sqrt(int x).

Compute and return the square root of x.


### Thoughts:



The most straight forward way it so iterate over all possible numbers, namely 1 to x/2+1.

But we could find it faster by using binary search. improving running time from O(x) to O(logx).

Plus, the condition to determine result is also critical, because we cannot say m*m == x is the checking condition.


### Solutions:

```java
public class Solution {
    public int mySqrt(int x) {
        int left = 1, right = x/2;
        while ( left <= right) {
            int mid = (left + right) /2;
            if (mid > x /mid) {
                right = mid - 1;
                continue;
            }
            if ((mid+1) <= x/(mid+1)) {
                left = mid + 1;
                continue;
            }
            return mid;
        }
        return x;
    }
}
```