# 153 Find Minimum in Rotated Sorted Array – Medium


### Problem:



Suppose a sorted array is rotated at some pivot unknown to you beforehand.

(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).

Find the minimum element.

You may assume no duplicate exists in the array.


### Thoughts:



Using a O(n) iteration to find the min value in the array is too trivial and straight forward.
So it is already clear enough that a Binary Search is needed here.

So this is a problem of modified Binary Search.


### Solutions:


```
public class Solution {
    public int findMin(int[] nums) {
        if (nums == null || nums.length ==0) {
            return -1;
        }
        if (nums[0] <= nums[nums.length - 1]) {
            return nums[0];
        }
        return bs(nums, 0, nums.length - 1);
    }
    private int bs(int[] nums, int start, int end) {
        if (start == end) {
            return nums[start];
        }
        int mid = (start + end) / 2;
        if (mid > 0 && nums[mid -1] > nums[mid]) {
            return nums[mid];
        }
        if (nums[mid] >= nums[0]) {
            return bs(nums, mid + 1, end);
        }
        else {
            return bs(nums, start, mid - 1);
        }
         
    }
}
```
non-Recursion:
```java
public class Solution {
    /**
     * @param nums: a rotated sorted array
     * @return: the minimum number in the array
     */
    public int findMin(int[] nums) {
        if (nums == null || nums.length == 0) {
            return -1;
        }
        
        int start = 0, end = nums.length - 1;
        int target = nums[nums.length - 1];
        
        // find the first element <= target
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (nums[mid] <= target) {
                end = mid;
            } else {
                start = mid;
            }
        }
        if (nums[start] <= target) {
            return nums[start];
        } else {
            return nums[end];
        }
    }
}
```