# 494 Target Sum

### Problem:

You are given a list of non-negative integers, a1, a2, ..., an, and a target, S. Now you have 2 symbols + and -. For each integer, you should choose one from + and - as its new symbol.

Find out how many ways to assign symbols to make sum of integers equal to target S.

Example 1:
```
Input: nums is [1, 1, 1, 1, 1], S is 3. 
Output: 5
Explanation: 

-1+1+1+1+1 = 3
+1-1+1+1+1 = 3
+1+1-1+1+1 = 3
+1+1+1-1+1 = 3
+1+1+1+1-1 = 3

There are 5 ways to assign symbols to make the sum of nums be target 3.
```

Note:
1. The length of the given array is positive and will not exceed 20.
2. The sum of elements in the given array will not exceed 1000.
3. Your output answer is guaranteed to be fitted in a 32-bit integer.


### Solutions:

```java
public class Solution {
    public int findTargetSumWays(int[] nums, int S) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        HashMap<Integer, Integer> count = new HashMap<Integer, Integer>();
        for (int i = 0; i < nums.length; i ++) {
            HashMap<Integer, Integer> newCount = new HashMap<Integer, Integer>();
            if (i == 0) {
                if (nums[i] == 0) {
                    newCount.put(0, 2);
                }
                else {
                    newCount.put(nums[i], 1);
                    newCount.put(-nums[i], 1);
                }
            }
            else {
                for (Integer sum:count.keySet()) {
                    int plus = count.get(sum);
                    if (newCount.containsKey(sum + nums[i])) {
                        plus += newCount.get(sum + nums[i]);
                    }
                    newCount.put(sum + nums[i], plus);
                    int minus = count.get(sum);
                    if (newCount.containsKey(sum - nums[i])) {
                        minus += newCount.get(sum - nums[i]);
                    }
                    newCount.put(sum - nums[i], minus);
                }
            }
            count = newCount;
        }
        if (count.containsKey(S)) {
            return count.get(S);
        }
        return 0;
    }
}
```