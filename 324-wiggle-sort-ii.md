# 324. Wiggle Sort II

### Problem:

Given an unsorted array nums, reorder it such that nums[0] < nums[1] > nums[2] < nums[3]....

Example:
(1) Given nums = [1, 5, 1, 1, 6, 4], one possible answer is [1, 4, 1, 5, 1, 6]. 
(2) Given nums = [1, 3, 2, 2, 3, 1], one possible answer is [2, 3, 1, 3, 1, 2].

Note:
You may assume all input has valid answer.

Follow Up:
Can you do it in O(n) time and/or in-place with O(1) extra space?

### Solutions:

```java
public class Solution {
    public void wiggleSort(int[] nums) {
        int[] tmp = new int[nums.length];
        Arrays.sort(nums);
        int left = (nums.length - 1) / 2, right = nums.length - 1;
        for (int i = 0; i < tmp.length; i ++) {
            if (i % 2 == 0) {
                tmp[i] = nums[left--];
            }
            else {
                tmp[i] = nums[right--];
            }
        }
        for (int i = 0; i < tmp.length; i ++) {
            nums[i] = tmp[i];
        }
    }
}
```

