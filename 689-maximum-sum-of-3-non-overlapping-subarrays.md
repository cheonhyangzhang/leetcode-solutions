# 689 Maximum Sum of 3 Non-Overlapping Subarrays

### Problem
In a given array nums of positive integers, find three non-overlapping subarrays with maximum sum.

Each subarray will be of size k, and we want to maximize the sum of all 3*k entries.

Return the result as a list of indices representing the starting position of each interval (0-indexed). If there are multiple answers, return the lexicographically smallest one.

Example:
```
Input: [1,2,1,2,6,7,5,1], 2
Output: [0, 3, 5]
Explanation: Subarrays [1, 2], [2, 6], [7, 5] correspond to the starting indices [0, 3, 5].
We could have also taken [2, 1], but an answer of [1, 3, 5] would be lexicographically larger.
```

Note:
nums.length will be between 1 and 20000.
nums[i] will be between 1 and 65535.
k will be between 1 and floor(nums.length / 3).


### Solutions

```java
class Solution {
    public int[] maxSumOfThreeSubarrays(int[] nums, int k) {
        int[] res = new int[3];
        int[] sums = new int[nums.length + 1];
        int sum = 0;
        for (int i = 0; i < nums.length; i ++) {
            sum += nums[i];
            sums[i + 1] = sum;
        }
        int[][] rsums = new int[nums.length][3];
        int[][] rindexes = new int[nums.length][3];
        for (int i = 0; i < 3; i ++) {
            for (int j = i * k; j + k - 1 < nums.length; j ++) {
                int lastRound = 0;
                if (i > 0 && j - 1 >= 0) {
                    lastRound = rsums[j - 1][i - 1];
                }
                int cand = getSum(sums, j, j + k - 1) + lastRound;
                int pre = 0;
                if (j + k - 2 >= 0) {
                    pre = rsums[j + k - 2][i];
                }
                if (cand > pre) {
                    rsums[j + k - 1][i] = cand;
                    rindexes[j + k - 1][i] = j;
                }
                else {
                    rsums[j + k - 1][i] = pre;
                    rindexes[j + k - 1][i] = rindexes[j + k - 2][i];
                }
            }
        }
        int tmp = rindexes[nums.length - 1][2];
        res[2] = tmp;
        tmp = rindexes[tmp - 1][1];
        res[1] = tmp;
        tmp = rindexes[tmp - 1][0];
        res[0] = tmp;
        return res;
        
    }
    private int getSum(int[] sums, int start, int end) {
        return sums[end + 1] - sums[start];
    }
}
```