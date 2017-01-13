# 283. Move Zeroes

### Problem:

Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.

For example, given nums = [0, 1, 0, 3, 12], after calling your function, nums should be [1, 3, 12, 0, 0].

Note:
You must do this in-place without making a copy of the array.
Minimize the total number of operations.

### Solutions:

```java
public class Solution {
    public void moveZeroes(int[] nums) {
        int cut = -1; // the left of cut is all non-zero
        for (int i = 0; i < nums.length; i ++) {
            if (nums[i] != 0) {
               if (i != cut + 1) {
                   while (cut < 0 || nums[cut]!=0) {
                       cut ++;
                   }
                   nums[cut] = nums[i];
                   nums[i] = 0;
               }
               else {
                   cut ++;
               }
            }
        }
    }
}
```