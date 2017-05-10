# 191 Number of 1 Bits – Easy

### Problem:
Write a function that takes an unsigned integer and returns the number of ’1′ bits it has (also known as the Hamming weight).

For example, the 32-bit integer ’11′ has binary representation 00000000000000000000000000001011, so the function should return 3.

### Thoughts:
This is very simple and straight forward. Just have a pivot integer, which iterates over all single bit integer of 32-bit.

### Solutions:

```java
public class Solution {
    // you need to treat n as an unsigned value
    public int hammingWeight(int n) {
        int pivot = 1;
        int sum = 0;
        for (int i = 0; i < 32; i ++){
            int p = pivot << i;
            if ((n & p) == p)
                sum ++;
        }
        return sum;
    }
}
```

```java
public class Solution {
    // you need to treat n as an unsigned value
    public int hammingWeight(int n) {
        int mask = 1;
        int count = 0;
        for (int i = 0; i < 32; i ++) {
            if ((n & mask) != 0) {
                count ++;
            }
            mask = (mask << 1);
        }
        return count;
    }
}
```