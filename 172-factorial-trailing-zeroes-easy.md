# 172 Factorial Trailing Zeroes – Easy


### Problem:
Given an integer n, return the number of trailing zeroes in n!.

Note: Your solution should be in logarithmic time complexity.

### Thoughts:
The number of trailing zeroes is determined by factor of 2 and 5.

IN the factorial of n, e. g. 1, 2, 3, 4, 5, 6, 7, …

there are always more 2 than 5, here 4 is considered to be 2 x 2.

So the number of trailing 0 is determined by number of 5.

Also note that, 25 works as two 5. So it should counted twice.

### Solutions:

```java
public class Solution {
    public int trailingZeroes(int n) {
        int result = 0;
        while (n != 0) {
            n = n / 5;
            result += n;
        }
        return result;
    }
}
```