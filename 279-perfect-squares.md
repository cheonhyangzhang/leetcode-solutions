# 279 Perfect Squares

### Problem:

Given a positive integer n, find the least number of perfect square numbers (for example, 1, 4, 9, 16, ...) which sum to n.

For example, given n = 12, return 3 because 12 = 4 + 4 + 4; given n = 13, return 2 because 13 = 4 + 9.

### Solutions:

```java
public class Solution {
    private HashMap<Integer, Integer> data = new HashMap<Integer, Integer>();;
    public int numSquares(int n) {
        if (data.containsKey(n)) {
            return data.get(n);
        }
        int up = (int)(Math.sqrt(n));
        if (up * up == n) {
            data.put(n, 1);
            return 1;
        }
        int min = Integer.MAX_VALUE;
        for (int i = up; i > 0; i --) {
            int tmp = 1 + numSquares(n - i * i);
            min = Math.min(min, tmp);
        }
        data.put(n, min);
        return min;
   
    }
}
```

```java
public class Solution {
    public int numSquares(int n) {
        int[] nums = new int[n + 1];
        for (int i = 1; i < n + 1; i ++) {
            nums[i] = Integer.MAX_VALUE;
        }
        int up = (int) Math.sqrt(n);
        for (int i = 1; i < n + 1; i ++) {
            for (int j = 1; j <= up && j * j <= i; j ++) {
                if (j * j == i) {
                    nums[i] = 1;
                }
                else {
                    nums[i] = Math.min(nums[i], nums[i - j * j] + 1);
                }
            }
        }
        return nums[n];
    }
}
```