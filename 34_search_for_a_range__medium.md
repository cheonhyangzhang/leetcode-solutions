# 34 Search for a Range – Medium


### Problem:



Given a sorted array of integers, find the starting and ending position of a given target value.

Your algorithm’s runtime complexity must be in the order of O(log n).

If the target is not found in the array, return [-1, -1].

For example,
Given [5, 7, 7, 8, 8, 10] and target value 8,
return [3, 4].


### Thoughts:


Easy to solve problem if using iteration to find the starting point and ending point. This approach will end up with O(n) running time.

However, there is a better approach which will be O(lgn) using binary search. Still, it’s okay to start with a straight forward method first, then think about optimization or a better approach.

### Solutions:
```java
public class Solution {
    public int[] searchRange(int[] nums, int target) {
        int[] result = searchR(nums, 0, nums.length - 1, target, 0);
        return result;
    }
    private int[] searchR(int[] nums, int start, int end, int target, int direction) {
        int[] result = new int[]{-1, -1};
        if (start > end) {
            return result;
        }
        int mid = (start + end) /2;
        if (nums[mid] < target) {
            return searchR(nums, mid + 1, end, target, 0);            
        }
        if (nums[mid] > target) {
            return searchR(nums, start, mid - 1, target, 0);
        }
        // nums[mid] == targe
        if (direction != 1) {
            int[] left = searchR(nums, start, mid-1, target, -1);
            result[0] = left[0] == -1?mid:left[0];
        }
        if (direction != -1) {
            int[] right = searchR(nums, mid+1, end, target, 1);
            result[1] = right[1] == -1?mid:right[1];
        }
     
        return result;
        
    }
}
```

```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;
        int[] res = new int[2];
        res[0] = -1;
        boolean has = false;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] < target) {
                left ++;
            }
            else if (nums[mid] == target) {
                has = true;
                right --;
            }
            else {
                right --;
            }
        }
        if (has) {
            res[0] = left;
        }
        left = 0;
        right = nums.length - 1;
        while (left <= right) { 
            int mid = left + (right - left) / 2;
            if (nums[mid] <= target) {
                left ++;
            }
            else {
                right --;
            }
        }
        if (has) {
            res[1] = right;
        }
        return res;
    }
}
```