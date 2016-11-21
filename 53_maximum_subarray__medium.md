# 53 Maximum Subarray – Medium


### Problem:



Find the contiguous subarray within an array (containing at least one number) which has the largest sum.

For example, given the array [−2,1,−3,4,−1,2,1,−5,4],
the contiguous subarray [4,−1,2,1] has the largest sum = 6.


### Thoughts:



If for an array max, max[i] stands for the maximum subarray ending at position i. So that max[i] = Math.max(max[i-1], nums[i]). But all we need is the maximum subarray for the whole array. So that we even don’t need the actual array. Just use a temp variable to keep the previous max value.


### Solutions:


```java
public class Solution {
    public int maxSubArray(int[] nums) {
        int currSum = 0;
        int max = Integer.MIN_VALUE;
        for (int i = 0; i < nums.length; i ++) {
            currSum = Math.max(currSum + nums[i], nums[i]);
            max = Math.max(currSum, max);
        }
        return max;
    }
}
```