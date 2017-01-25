# 360. Sort Transformed Array

### Problem:

<pre>
Given a sorted array of integers nums and integer values a, b and c. Apply a function of the form f(x) = ax2 + bx + c to each element x in the array.

The returned array must be in sorted order.

Expected time complexity: O(n)

Example:
nums = [-4, -2, 2, 4], a = 1, b = 3, c = 5,

Result: [3, 9, 15, 33]

nums = [-4, -2, 2, 4], a = -1, b = 3, c = 5

Result: [-23, -5, 1, 7]
</pre>

### Solutions:

```java
public class Solution {
    public int[] sortTransformedArray(int[] nums, int a, int b, int c) {
        if (a == 0) {
            return straight(nums, a, b, c);    
        }
        else {
            return curve(nums, a, b, c);
        }
    }
    private int[] straight(int[] nums, int a, int b, int c) {
        int[] result = new int[nums.length];
        for (int i = 0; i < nums.length; i ++) {
            if (b > 0) {
                result[i] = nums[i] * b + c;
            }
            else {
                result[nums.length - 1 - i] = nums[i] * b + c;
            }
        }
        return result;
    }
    private int[] curve(int[] nums, int a, int b, int c) {
        double mid = (0.0 - (double)b) / (2.0 * (double)a);
        int[] result = new int[nums.length];
        double min = Double.MAX_VALUE;
        int center = 0;
        for (int i = 0; i < nums.length; i ++) {
            double diff = Math.abs(nums[i] - mid);
            if (diff < min) {
                min = diff;
                center = i;
            }
        }
        int left = center, right = center;
        for (int i = 0; i < nums.length; i ++) {
            int x = 0;
            if (left == center) {
                x = nums[left];
                left --;
                right ++;
            }
            else if (left < 0) {
                x = nums[right];
                right ++;
            }
            else if (right >= nums.length) {
                x = nums[left];
                left --;
            }
            else {
                double leftDiff = Math.abs((double)nums[left] - mid);
                double rightDiff = Math.abs((double)nums[right] - mid);
                if (leftDiff < rightDiff) {
                    x = nums[left];
                    left --;
                }
                else {
                    x = nums[right];
                    right ++;
                }
            }
            if (a > 0) {
                result[i] = a * x * x + b * x + c;
            }
            else {
                result[nums.length - i - 1] = a * x * x + b * x + c;
            }
        }
        return result;
    }
}
```
```java
public class Solution {
    public int[] sortTransformedArray(int[] nums, int a, int b, int c) {
        int[] result = new int[nums.length];
        int left = 0, right = result.length - 1;
        for (int i = 0; i < result.length; i ++) {
            if (a > 0 || (a == 0 && b < 0)) {
                int leftp = a * nums[left] * nums[left] + b * nums[left] + c;
                int rightp = a * nums[right] * nums[right] + b * nums[right] + c;
                if (leftp > rightp) {
                    result[result.length - 1 - i] = leftp;
                    left ++;
                }
                else {
                    result[result.length - 1 - i] = rightp;
                    right --;
                }
                
            }
            else {
                int leftp = a * nums[left] * nums[left] + b * nums[left] + c;
                int rightp = a * nums[right] * nums[right] + b * nums[right] + c;
                if (leftp < rightp) {
                    result[i] = leftp;
                    left ++;
                }
                else {
                    result[i] = rightp;
                    right --;
                }
            }
        }
        return result;
    }
}
```