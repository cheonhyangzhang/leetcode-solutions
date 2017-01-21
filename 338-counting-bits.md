# 338. Counting Bits

### Problem:

Given a non negative integer number num. For every numbers i in the range 0 ≤ i ≤ num calculate the number of 1's in their binary representation and return them as an array.

Example:
For num = 5 you should return [0,1,1,2,1,2].

Follow up:

It is very easy to come up with a solution with run time O(n*sizeof(integer)). But can you do it in linear time O(n) /possibly in a single pass?
Space complexity should be O(n).
Can you do it like a boss? Do it without using any builtin function like __builtin_popcount in c++ or in any other language.
Hint:

You should make use of what you have produced already.
Divide the numbers in ranges like [2-3], [4-7], [8-15] and so on. And try to generate new range from previous.
Or does the odd/even status of the number help you in calculating the number of 1s?

### Solutions:

```java
public class Solution {
    public int[] countBits(int num) {
        int[] result = new int[num + 1];
        int[] base = new int[]{0, 1, 1, 2};
        if (num <= 3) {
            for (int i = 0; i <= num; i ++) {
                result[i] = base[i];
            }
           return result; 
        }
        int diff = 2;
        int add = 0;
        int start = 4;
        int j = start - diff;
        for (int i = 0; i <= 3; i ++) {
            result[i] = base[i];
        }
        for (int i = 4; i <= num; i ++) {
            result[i] = result[j] + add;
            j ++;
            if (j == start) {
                if (add == 0) {
                    add = 1;
                    j = start - diff;
                }
                else {
                    add = 0;
                    diff = diff << 1;
                    start = i + 1;
                    j = start - diff;
                }
            }
        }
        return result;
    }
}
```

```java

```