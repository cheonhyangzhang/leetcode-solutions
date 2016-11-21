# 35 Search Insert Position – Medium


### Problem:



Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You may assume no duplicates in the array.

Here are few examples.
[1,3,5,6], 5 → 2
[1,3,5,6], 2 → 1
[1,3,5,6], 7 → 4
[1,3,5,6], 0 → 0


### Thoughts:



This problem could be solved easily by iterating over the list. This will end up with O(n).

But there could be a better solution which is O(lgn) using modified binary search.


### Solutions:



```java
public class Solution {
    public int searchInsert(int[] nums, int target) {
        return bs(nums, 0, nums.length -1, target);
    }
    private int bs(int[]nums, int start, int end, int target) {
        if (start > end) {
            return end + 1;
        }
        int mid = (start + end) / 2;
        if (nums[mid] < target) {
            return bs(nums, mid + 1, end, target);
        }
        if (nums[mid] > target) {
            return bs(nums, start, mid - 1, target);
        }
        return mid;
    }
}
```