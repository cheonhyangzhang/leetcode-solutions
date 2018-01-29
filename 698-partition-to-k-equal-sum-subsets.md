# 698 Partition to K Equal Sum Subsets

### Problem
Given an array of integers nums and a positive integer k, find whether it's possible to divide this array into k non-empty subsets whose sums are all equal.

Example 1:
```
Input: nums = [4, 3, 2, 3, 5, 2, 1], k = 4
Output: True
Explanation: It's possible to divide it into 4 subsets (5), (1, 4), (2,3), (2,3) with equal sums.
```
Note:

1 <= k <= len(nums) <= 16.
0 < nums[i] < 10000.

### Solutions
```java
class Solution {
    public boolean canPartitionKSubsets(int[] nums, int k) {
        int sum = 0;
        for (int i = 0; i < nums.length; i ++) {
            sum += nums[i];
        }
        if (sum % k != 0) {
            return false;
        }
        Arrays.sort(nums);
        boolean[] visited = new boolean[nums.length];
        return process(0, nums, visited, sum/k, sum/k, k);
    }
    private boolean process(int start, int[] nums, boolean[] visited, int sum, int left, int togo) {
        if (togo == 1) {
            return true;
        }
        if (left == 0) {
            return process(0, nums, visited, sum, sum, togo - 1);
        }
        for (int i = start; i < nums.length; i ++) {
            if (nums[i] > left) {
                return false;
            }
            if (visited[i] == true) {
                continue;
            }
            visited[i] = true;
            if (process(i + 1, nums, visited, sum, left - nums[i], togo)) {
                return true;
            }
            visited[i] = false;
        }
        return false;
    }
    
}
```

