# 81 Leetcode Java Search in Rotated Sorted Array II


### Problem: 


Version I:
Suppose a sorted array is rotated at some pivot unknown to you beforehand.

(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).

You are given a target value to search. If found in the array return its index, otherwise return -1.

You may assume no duplicate exists in the array.

Follow up for “Search in Rotated Sorted Array”:
What if duplicates are allowed?

Would this affect the run-time complexity? How and why?


### Thoughts: 


In version I we use condition to check if left half or right half is sorted. This depends on element doesn’t have duplicate.
When it allows duplicates, e.g
[1, 3, 1, 1, 1],
nums[start] <= nums[mid] is not good enough to say left half is sorted.
We can only use nums[start] < nums[mid] to say left half is sorted.
Then what about nums[start] = nums[mid]?
When that happens, we can only say the target is not in nums[start], and that' all we can know so far. So we just increase start index in this case.

With that being said, the worst case would be end up with O(n). which means you have to check every single element in the array.


### Solution:



```
public class Solution {
    public boolean search(int[] nums, int target) {
        int start = 0, end = nums.length - 1;
        while (start <= end) {
            int mid = ( start + end) / 2;
            if (nums[mid] == target) {
                return true;
            }
            if (nums[start] < nums[mid]) {
                if (nums[start] <= target && target < nums[mid]) {
                    end = mid -1;
                }
                else {
                    start = mid + 1;
                }
            }
            else if (nums[start] > nums[mid]) {
                if (nums[mid] < target && target <= nums[end]) {
                    start = mid + 1;
                }
                else {
                    end = mid -1;
                }
            }
            else {
                start ++;
            }
        }
        return false;
    }
}
```
