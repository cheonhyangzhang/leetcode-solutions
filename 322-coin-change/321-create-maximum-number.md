# 321 Create Maximum Number

### Problem:

Given two arrays of length m and n with digits 0-9 representing two numbers. Create the maximum number of length k <= m + n from digits of the two. The relative order of the digits from the same array must be preserved. Return an array of the k digits. You should try to optimize your time and space complexity.

Example 1:
nums1 = [3, 4, 6, 5]
nums2 = [9, 1, 2, 5, 8, 3]
k = 5
return [9, 8, 6, 5, 3]

Example 2:
nums1 = [6, 7]
nums2 = [6, 0, 4]
k = 5
return [6, 7, 6, 0, 4]

Example 3:
nums1 = [3, 9]
nums2 = [8, 9]
k = 3
return [9, 8, 9]

### Solutions:

```java
public class Solution {
    public int[] maxNumber(int[] nums1, int[] nums2, int k) {
        int[] result = new int[k];
        for (int i = Math.max(0, k - nums2.length); i <= Math.min(nums1.length, k); i ++) {
            int j = k - i;
            // pick i numbers from nums1 and pick j numbers from nums2
            int[] part1 = findMax(nums1, i);
            int[] part2 = findMax(nums2, j);
            int[] cand = merge(part1, part2);
            if (greater(cand, 0, result, 0)) {
                result = cand;
            }
        }
        return result;
    }
    private boolean greater(int[] nums1, int start1, int[] nums2, int start2) {
        int i = start1, j = start2;
        while (i < nums1.length && j < nums2.length) {
            if (nums1[i] > nums2[j]) {
                return true;
            }
            if (nums1[i] < nums2[j]) {
                return false;
            }
            i ++;
            j ++;
        }
        if (i < nums1.length) {
            return true;
        }
        else {
            return false;
        }
    }
    private int[] merge(int[] nums1, int[] nums2) {
        int[] result = new int[nums1.length + nums2.length];
        int i = 0, j = 0;
        for (int k = 0; k < nums1.length + nums2.length; k ++) {
            if (greater(nums1, i, nums2, j)) {
                result[k] = nums1[i];
                i ++;
            }
            else {
                result[k] = nums2[j];
                j ++;
            }
        }
        return result;
    }
    private int[] findMax(int[] nums, int k) {
        int[] result = new int[k];
        int j = 0;
        for (int i = 0; i < nums.length; i ++) {
            while (j > 0 && result[j - 1] < nums[i] && j + nums.length - i > k) {
                j --;
            }
            if (j < k) {
                result[j] = nums[i];
                j ++;
            }
            
        }
        return result;
    }
}
```