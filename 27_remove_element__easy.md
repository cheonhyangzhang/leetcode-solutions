# 27 Remove Element – Easy


### Problem:



Given an array and a value, remove all instances of that value in place and return the new length.

The order of elements can be changed. It doesn’t matter what you leave beyond the new length.


### Thoughts:


This problem could be solved in O(n). But it’s always good to come up with a solution that is as good as possible, even inside of O(n) time. Solution below is following the principle that only do the swap that’s necessary.


### Solutions:


```java
public class Solution {
    public int removeElement(int[] nums, int val) {
        int start = 0, end = nums.length -1;
        while (start <= end) {
            if (nums[start] != val) {
                start ++;
                continue;
            }
            if (nums[end] == val) {
                end --;
                continue;
            }
            nums[start] = nums[end];
            start ++;
            end --;
        }
        return start;
    }
}
```