# 189 Rotate Array – Easy

### Problem:
Rotate an array of n elements to the right by k steps.

For example, with n = 7 and k = 3, the array [1,2,3,4,5,6,7] is rotated to [5,6,7,1,2,3,4].

Note:
Try to come up as many solutions as you can, there are at least 3 different ways to solve this problem.

Hint:
Could you do it in-place with O(1) extra space?

### Thoughts:
This problem is marked as easy but since it requires 3 solutions which makes it a little bit harder.

Solution 1: Create a new array, for each element of the original array, calculate the expected index in the new array. Then copy the new array into the origianl array. Note that this requires O(n) space.

Solution 2: Similar strategy as we used in Reverse Words in String II, reverse the whole array, then reverse the array for 0…k-1, and k…n-1.

Solution 3: Replace the element step by step. Start with element with index 0, keep the value of current. The expected index for 0 is 0 + k, but before overwrite nums[0+k], keep it in current. Another thing to avoid is for this case, [1, 2, 3, 4] while k is 2, then it will try with sequence 1->3->1->3… and it will never stop. In order to avoid this we need to determine when this happens, we start with 2 again, so that sequence 2->4 will do the remaining job.

### Solutions:

```java
public class Solution {
    public void rotate(int[] nums, int k) {
        if (nums.length == 0) {
            return;
        }
        k = k % nums.length;
        rotate1(nums, k);
        rotate2(nums, k);
        rotate3(nums, k);
    }
    private void rotate3(int[] nums, int k) {
        int curr = nums[0];
        int index = 0;
        int distance = 0;
        for (int i = 0; i < nums.length; i ++) {
            index = (index + k) % nums.length;
            int tmp = nums[index];
            nums[index] = curr;
            curr = tmp;
            distance = (distance + k) % nums.length;
            if (distance == 0) {
                index = (index + 1) % nums.length;
                curr = nums[index];
            }
        }
    }
    private void rotate2(int[] nums, int k) {
        reverse(nums, 0, nums.length - 1);
        reverse(nums, 0, k - 1);
        reverse(nums, k, nums.length - 1);
    }
    private void reverse(int[] nums, int i, int j) {
        while (i < j) {
            int tmp = nums[i];
            nums[i] = nums[j];
            nums[j] = tmp;
            i ++;
            j --;
        }
    }
    private void rotate1(int[] nums, int k) {
        int[] newSums = new int[nums.length];
        for (int i = 0; i < nums.length; i ++) {
            int j = (i + k) % nums.length;
            newSums[j] = nums[i];
        }
        for (int i = 0; i < nums.length; i ++) {
            nums[i] = newSums[i];
        }
    }
}
```