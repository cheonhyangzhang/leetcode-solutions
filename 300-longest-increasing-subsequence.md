# 300 Longest Increasing Subsequence

### Problem:

Given an unsorted array of integers, find the length of longest increasing subsequence.

For example,
Given [10, 9, 2, 5, 3, 7, 101, 18],
The longest increasing subsequence is [2, 3, 7, 101], therefore the length is 4. Note that there may be more than one LIS combination, it is only necessary for you to return the length.

Your algorithm should run in O(n2) complexity.

Follow up: Could you improve it to O(n log n) time complexity?

### Solutions:

```java
public class Solution {
    public int lengthOfLIS(int[] nums) {
        if(nums.length == 0) {
            return 0;
        }
        int[] dp = new int[nums.length];
        dp[0] = 1;
        int max = 1;
        for (int i = 1; i < nums.length; i ++) {
            int tmp = 1;
            for (int j = i - 1; j >=0; j --) {
                if (nums[j] < nums[i]) {
                    tmp = Math.max(dp[j] + 1, tmp);
                }
            }
            dp[i] = tmp;
            max = Math.max(tmp, max);
        }
        return max;
    }
}
```

