# 162 Find Peak Element – Medium
### Problem:

A peak element is an element that is greater than its neighbors.

Given an input array where num[i] ≠ num[i+1], find a peak element and return its index.

The array may contain multiple peaks, in that case return the index to any one of the peaks is fine.

You may imagine that num[-1] = num[n] = -∞.

For example, in array [1, 2, 3, 1], 3 is a peak element and your function should return the index number 2.

click to show spoilers.

Note:Your solution should be in logarithmic complexity.

### Thoughts:

Trivial way is to use a O(n) iteration, then a peak element could be found.

However, a better solution with O(nlogn) exists. A modified binary search. When hit the mid, move to the lower half.

Binary search could be implemented in a recursion way or in an iterative way. Below is using an iterative way.

### Solutions:

```java
public class Solution {
    public int findPeakElement(int[] nums){
        if (nums == null)
            return -1;
        if (nums.length == 1)
            return 0;
        int start = 0;
        int end = nums.length - 1;
        while (start <= end){
            int mid = (start + end) /2;
            if ((mid == 0 || nums[mid - 1] < nums[mid]) && (mid == nums.length - 1 || nums[mid] > nums[mid + 1]))
                return mid;
            else if (mid > 0 && nums[mid - 1] > nums[mid])
                end = mid - 1;
            else
                start = mid + 1;
            }
        return -1;
    }
}
```
Updated: 12/24/2016
Alternative recursion solution:

```java
public class Solution {
    public int findPeakElement(int[] nums){
        return bs(nums, 0, nums.length - 1);    
    }
    private int get(int[] nums, int i) {
        if (i < 0 || i > nums.length - 1) {
            return Integer.MIN_VALUE;
        }
        return nums[i];
    }
    private int bs(int[] nums, int start, int end) {
        if (start == end) {
            return start;
        }
        int mid = (start + end) / 2;
        if (get(nums, mid) > get(nums, mid - 1) && get(nums, mid) > get(nums, mid + 1)) {
            return mid;
        }
        if (get(nums, mid) < get(nums, mid - 1)) {
            return bs(nums, start, mid - 1);
        } 
        else {
            return bs(nums, mid + 1, end);
        }
    }
}
```