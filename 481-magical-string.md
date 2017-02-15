# 481. Magical String

### Problem:
A magical string S consists of only '1' and '2' and obeys the following rules:

The string S is magical because concatenating the number of contiguous occurrences of characters '1' and '2' generates the string S itself.

The first few elements of string S is the following: S = "1221121221221121122……"

If we group the consecutive '1's and '2's in S, it will be:

1 22 11 2 1 22 1 22 11 2 11 22 ......

and the occurrences of '1's or '2's in each group are:

1 2	2 1 1 2 1 2 2 1 2 2 ......

You can see that the occurrence sequence above is the S itself.

Given an integer N as input, return the number of '1's in the first N number in the magical string S.

Note: N will not exceed 100,000.

Example 1:
```
Input: 6
Output: 3
Explanation: The first 6 elements of magical string S is "12211" and it contains three 1's, so return 3.
```

### Solutions:

```java
public class Solution {
    public int magicalString(int n) {
        if (n <= 0) {
            return 0;
        }
        int[] data = new int[100002];
        data[0] = 1;
        int i = 0, j = 0;
        int count = 1;
        while (i < n) {
            if (data[j] == 1) {
                if (data[i] == 1) {
                    data[++i] = 2;
                }
                else {
                    data[++i] = 1;
                    if (i < n) {
                        count ++;
                    }
                }
            }
            else {
                if (data[i] == 1) {
                    data[++i] = 1;
                    if (i < n) {
                        count ++;
                    }
                    data[++i] = 2;
                }
                else {
                    data[++i] = 2;
                    data[++i] = 1;
                    if (i < n) {
                        count ++;
                    }
                }
            }
            j ++;
        }
        return count;
    }
}
```

```java
public class Solution {
    public int magicalString(int n) {
        if (n <= 0) {
            return 0;
        }
        if (n <= 3) {
            return 1;
        }
        int[] data = new int[100002];
        data[0] = 1;
        data[1] = 2;
        data[2] = 2;
        
        int i = 2, j = 2;
        int count = 1;
        int num = 1;
        while (i < n) {
            for (int k = 0; k < data[j]; k ++) {
                data[++i] = num;
                if (num == 1 && i < n) {
                    count ++;
                }
            }
            j ++;
            num = num ^ 3;
        }
        return count;
    }
}
```

```java
public class Solution {
    public int magicalString(int n) {
        if (n <= 0) {
            return 0;
        }
        if (n <= 3) {
            return 1;
        }
        StringBuilder sb = new StringBuilder("122");
        int i = 2;
        while (sb.length() < n) {
            int num = (sb.charAt(sb.length() - 1) - '0') ^ 3;
            int repeat = sb.charAt(i) - '0';
            for (int j = 0; j < repeat; j ++) {
                sb.append(num);
            }
            i ++;
        }
        int count = 0;
        for (i = 0; i < n; i ++) {
            if (sb.charAt(i) == '1') {
                count ++;
            }
        }
        return count;
    }
}
```