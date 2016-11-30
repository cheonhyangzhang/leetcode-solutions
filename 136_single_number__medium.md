# 136 Single Number – Medium


### Problem:



Given an array of integers, every element appears twice except for one. Find that single one.

Note:
Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?


### Thoughts:



This is surely a tricky question. It’s good to know how to solve. But I don’t think this is a good interview question, namely not a good question to measure a programmer’s problem solving skills.

Start with value 0, if there are two same number, when you do a XOR, you flip the bit twice which means the bit will remain 0. but for the unique number, the corresponding bit only flipped once, 0 -> 1, so the value will end up as the unique number.


### Solutions:



```java
public class Solution {
    public int singleNumber(int[] A) {
        int result = 0;
        for (int i = 0; i < A.length; i ++)
            result = result ^ A[i];
        return result;
    }
}
```