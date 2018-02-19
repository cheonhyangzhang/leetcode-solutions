# 360. Sort Transformed Array

### Problem:


Given a sorted array of integers nums and integer values a, b and c. Apply a function of the form f(x) = ax^2 + bx + c to each element x in the array.

The returned array must be in sorted order.

Expected time complexity: O(n)

Example:
nums = [-4, -2, 2, 4], a = 1, b = 3, c = 5,

Result: [3, 9, 15, 33]

nums = [-4, -2, 2, 4], a = -1, b = 3, c = 5

Result: [-23, -5, 1, 7]


### Solutions:

```java
public class Solution {
    public int[] sortTransformedArray(int[] nums, int a, int b, int c) {
        int[] result = new int[nums.length];
        int left = 0, right = result.length - 1;
        for (int i = 0; i < result.length; i ++) {
            if (a > 0) {
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