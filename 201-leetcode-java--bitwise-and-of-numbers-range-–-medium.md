# 201 LeetCode Java : Bitwise AND of Numbers Range – Medium

### Problem:

Given a range [m, n] where 0 <= m <= n <= 2147483647, return the bitwise AND of all numbers in this range, inclusive.

For example, given the range [5, 7], you should return 4.

### Thoughts:

The solution code is very easy but it’s not every easy to come up the idea in mind at the first glance of the problem.

For the given example, 5 – 7, which is 101, 110, 111, result is 100, which is 4.

Because we are applying AND to the bit, so as far as there is one 0, then the result for that bit is 0.

Keep this in mind, the result is determined by the same high bits of the starting and ending number,

so for 101, 111, they are same in the first 1 bit, so the result is 100.

### Solutions:

```java
public class Solution {
    public int rangeBitwiseAnd(int m, int n) {
        int offset = 0;
        while (true){
            if (m == n){
                return m << offset; 
            } 
            m >>= 1;
            n >>= 1;
            offset++;
        }
    }
}
```
Updated: 12/21/2016
Updated: Improve logic.

```java
public class Solution {
    public int rangeBitwiseAnd(int m, int n) {
        int offset = 0;
        while (m != n) {
            m = m >> 1;
            n = n >> 1;
            offset ++;
        }
        return m << offset;
    }
}
```