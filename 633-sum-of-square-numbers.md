# 633 Sum of Square Numbers

### Problem
Given a non-negative integer c, your task is to decide whether there're two integers a and b such that a2 + b2 = c.

Example 1:
```
Input: 5
Output: True
Explanation: 1 * 1 + 2 * 2 = 5
```

Example 2:
```
Input: 3
Output: False
```

### Solutions
```java
class Solution {
    public boolean judgeSquareSum(int c) {
        HashSet<Long> nums = new HashSet<>();
        for (int i = 0; i <= Math.sqrt(c); i ++) {
            nums.add((long)i*i);
            if (nums.contains((long)(c - i*i))) {
                return true;
            }
        }
        return false;
    }
}
```