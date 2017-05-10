# 190 Java: Reverse Bits – Easy


### Problem:
Reverse bits of a given 32 bits unsigned integer.

For example, given input 43261596 (represented in binary as 00000010100101000001111010011100), return 964176192 (represented in binary as00111001011110000010100101000000).

Follow up:
If this function is called many times, how would you optimize it?

### Thoughts:
There could be different ways to solve this problem.

The solution below is using a helper function swapBits which makes things a littler easier.

swapBits is responsible for swapping bits by given bit index.

### Solutions:

```java
public class Solution {
    // you need treat n as an unsigned value
    public int reverseBits(int n) {
        for (int i = 0; i < 16; i++) { 
            n = swapBits(n, i, 32 - i - 1); 
        } 
        return n; 
    } 
    public int swapBits(int n, int i, int j) { 
        int a = (n >> i) & 1;
        int b = (n >> j) & 1;
        if ((a ^ b) != 0) {
            return n ^= (1 << i) | (1 << j);
        }
 
        return n;
    }
}
```

```java
public class Solution {
    // you need treat n as an unsigned value
    public int reverseBits(int n) {
        int result = 0;
        int mask = 1;
        for (int i = 0; i < 32; i ++) {
            int digit = n & mask;
            result = (result << 1);
            if (digit != 0) {
                 result = result + 1;
            }
            mask = (mask << 1);
        }
        return result;
    }
}
```