# 670 Maximum Swap

### Problem

Given a non-negative integer, you could swap two digits at most once to get the maximum valued number. Return the maximum valued number you could get.

Example 1:
```
Input: 2736
Output: 7236
Explanation: Swap the number 2 and the number 7.
```
Example 2:
```
Input: 9973
Output: 9973
Explanation: No swap.
```
Note:
The given number is in the range [0, 108]

### Solutions

```java
class Solution {
    public int maximumSwap(int num) {
        StringBuilder sb = new StringBuilder();
        while (num > 0) {
            sb.insert(0, num % 10);
            num = num / 10;
        }
        char[] chars = sb.toString().toCharArray();
        char[] maxs = new char[chars.length];
        int[] indexes = new int[chars.length];
        for (int i = chars.length - 1; i >= 0; i --) {
            if (i == chars.length - 1) {
                maxs[i] = chars[i];
                indexes[i] = i;
            }
            else {
                if (chars[i] > maxs[i + 1]) {
                    maxs[i] = chars[i];
                    indexes[i] = i;
                }
                else {
                    maxs[i] = maxs[i + 1];
                    indexes[i] = indexes[i + 1];
                }
            }
        }
        for (int i = 0; i < chars.length; i ++) {
            if (maxs[i] > chars[i]) {
                //swap i and indexes[i];
                char c = chars[i];
                chars[i] = chars[indexes[i]];
                chars[indexes[i]] = c;
                break;
            }
        }
        int res = 0;
        for (int i = 0; i < chars.length; i ++) {
            res = res * 10 + (chars[i] - '0');
        }
        return res;
    }
}
```

