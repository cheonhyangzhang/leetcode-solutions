# 397 Integer Replacement

### Problem:

Given a positive integer n and you can do operations as follow:

If n is even, replace n with n/2.
If n is odd, you can replace n with either n + 1 or n - 1.
What is the minimum number of replacements needed for n to become 1?

Example 1:
```
Input:
8

Output:
3

Explanation:
8 -> 4 -> 2 -> 1
```

Example 2:
```
Input:
7

Output:
4

Explanation:
7 -> 8 -> 4 -> 2 -> 1
or
7 -> 6 -> 3 -> 2 -> 1
```

### Solutions:

```java
public class Solution {
    public int integerReplacement(int n) {
        HashMap<Long, Integer> result = new HashMap<Long, Integer>();
        return process(n, result);
    }
    private int process(long n, HashMap<Long, Integer> result) {
        if (result.containsKey(n)) {
            return result.get(n);
        }
        int count = 0;
        if (n == 1) {
            return 0;
        }
        if (n % 2 == 0) {
            count = process(n / 2, result) + 1;
        }
        else {
            count = Math.min(process(n - 1, result), process(n + 1, result)) + 1;
        }
        result.put(n, count);
        return count;
    }
}
```

```java
public class Solution {
    public int integerReplacement(int n) {
        long t = n;
        int cnt = 0;
        while (t > 1) {
            ++cnt;
            if ((t&1) == 1) {
                if (((t&2) == 2) && (t != 3)) ++t;
                else --t;
            } else {
                t >>= 1;
            }
        }
        return cnt;
    }
}
```