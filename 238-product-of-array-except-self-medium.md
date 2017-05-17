# 238 Product of Array Except Self – Medium

### Problem:
Given an array of n integers where n > 1, nums, return an array output such that output[i] is equal to the product of all the elements of nums except nums[i].

Solve it without division and in O(n).

For example, given [1,2,3,4], return [24,12,8,6].

Follow up:
Could you solve it with constant space complexity? (Note: The output array does not count as extra space for the purpose of space complexity analysis.)

### Thoughts:
This is a hard problem. First let’s think in a easy way, how can we solve without the requirement of constant space?
We create two helper array, one stores product from left to right and the other is from right to left. Say for the given example, [1, 2, 3, 4], left to right will be [1, 1×1, 1x1x2, 1x2x3], while right to left will be [2x3x4x1, 3x4x1, , 4×1, 1], so that when you multiply element from each of the two, you get the expected product for each element in the result, notice that each product will contains an additional 1. Left to right array need to initialize first element to be 1. Right to left array need to initialize last element to be 1.

Improved way needs to be using constant space. So we already have the result array, this means we need to solve the problem with one less array. Result will be used as ltor, then we use an additional variable to keep the calculated value that’s originally supposed to be filled in rtol.

### Solutions:

```java
public class Solution {
    public int[] productExceptSelf(int[] nums) {
        int[] result = new int[nums.length];
        result[0] = 1;
        for (int i = 1; i < nums.length; i ++) {
            result[i] = nums[i - 1] * result[i - 1];
        }
        int tmp = 1;
        for (int i = nums.length - 2; i >= 0; i --) {
            result[i] = result[i] * (nums[i + 1] * tmp);
            tmp = nums[i + 1] * tmp;
        }
        return result;
    }
}
```
