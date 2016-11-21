# 55 Jump Game – Medium


### Problem:



Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Determine if you are able to reach the last index.

For example:
A = [2,3,1,1,4], return true.

A = [3,2,1,0,4], return false.


### Thoughts:



Keep a variable to keep the current max jump.

During the iteration, if the current index i is less than current max jump, it means there is no way to jump to current index, so in this case, we should return false early.

Otherwise, if we could make it to the end, it means it’s possible to reach the end of the array. Then we should return true.


### Solutions:


```java
public class Solution {
    public boolean canJump(int[] nums) {
        int max = 0;
        for (int i = 0; i < nums.length; i ++) {
            if (i > max) {
                return false;
            }
            max = Math.max(max, i + nums[i]);
        }
        return true;
    }
}
```