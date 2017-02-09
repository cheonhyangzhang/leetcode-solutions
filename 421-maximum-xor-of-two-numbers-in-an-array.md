# 421. Maximum XOR of Two Numbers in an Array

### Problem:

Given a non-empty array of numbers, a0, a1, a2, … , an-1, where 0 ≤ ai < 231.

Find the maximum result of ai XOR aj, where 0 ≤ i, j < n.

Could you do this in O(n) runtime?

Example:
```
Input: [3, 10, 5, 25, 2, 8]

Output: 28

Explanation: The maximum result is 5 ^ 25 = 28.
```

### Solutions:
```java
public class Solution {
    public int findMaximumXOR(int[] nums) {
        int max = 0;
        int mask = 0;
        for (int i = 31; i >= 0; i --) {
            mask = mask|(1<<i);
            Set<Integer> prefix = new HashSet<Integer>();
            for (int j = 0; j < nums.length; j ++) {
                prefix.add(nums[j] & mask);
            }
            int cand = max|(1<<i);
            for (Integer pre:prefix) {
                if (prefix.contains(cand^pre)) {
                    max = cand;
                    break;
                }
            }
        }
        return max;
    }
}
```