# 264. Ugly Number II - Medium

### Problem:

Write a program to find the n-th ugly number.

Ugly numbers are positive numbers whose prime factors only include 2, 3, 5. For example, 1, 2, 3, 4, 5, 6, 8, 9, 10, 12 is the sequence of the first 10 ugly numbers.

Note that 1 is typically treated as an ugly number, and n does not exceed 1690.

Hint:

The naive approach is to call isUgly for every number until you reach the nth one. Most numbers are not ugly. Try to focus your effort on generating only the ugly ones.
An ugly number must be multiplied by either 2, 3, or 5 from a smaller ugly number.
The key is how to maintain the order of the ugly numbers. Try a similar approach of merging from three sorted lists: L1, L2, and L3.
Assume you have Uk, the kth ugly number. Then Uk+1 must be Min(L1 * 2, L2 * 3, L3 * 5).

### Solutions:

```java
public class Solution {
    public int nthUglyNumber(int n) {
        if (n <= 0) {
            return 0;
        }
        ArrayList<Integer> result = new ArrayList<Integer>();
        int two = 0;
        int three = 0;
        int five = 0;
        result.add(1);
        while (result.size() < n) {
            int m2 = result.get(two) * 2;
            int m3 = result.get(three) * 3;
            int m5 = result.get(five) * 5;
            int min = Math.min(m2, Math.min(m3, m5));
            result.add(min);
            if (m2 == min)
                two ++;
            if (m3 == min) 
                three ++;
            if (m5 == min)
                five ++;
        }
        return result.get(result.size() - 1);
    }
}
```