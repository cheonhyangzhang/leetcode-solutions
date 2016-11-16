# 16 3Sum Closest – Medium


### Problem:



Given an array S of n integers, find three integers in S such that the sum is closest to a given number, target. Return the sum of the three integers. You may assume that each input would have exactly one solution.

    For example, given array S = {-1 2 1 -4}, and target = 1.

    The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).

### Thoughts:



This is almost the same problem with 3Sum. The only difference is the checking condition. Instead of a + b + c = 0, check if (a + b + c – target) is min.


### Solutions:

```java
public class Solution {
    public int threeSumClosest(int[] nums, int target) {
        if (nums.length == 0){
            return 0;
        }
        Arrays.sort(nums);
        int min = Integer.MAX_VALUE;
        int closed = 0;
        for (int i = 0; i < nums.length; i ++){
            if (i == 0 || nums[i] != nums[i-1]){
                int start = i + 1;
                int end = nums.length - 1;
                while (start < end){
                    int sum = nums[i] + nums[start] + nums[end];
                    if (Math.abs(sum - target) < min){
                        min = Math.abs(sum - target);
                        closed = sum;
                    }
                    if (sum < target){ 
                        start ++; } 
                    else{ // >= target
                        end --;
                    }//if
                }//while
             }//if
        }//for
        return closed;
    }
}
```