# 167 Two Sum II – Input array is sorted – Medium

### Problem:
Given an array of integers that is already sorted in ascending order, find two numbers such that they add up to a specific target number.

The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2. Please note that your returned answers (both index1 and index2) are not zero-based.

You may assume that each input would have exactly one solution.

Input: numbers={2, 7, 11, 15}, target=9
Output: index1=1, index2=2

### Thoughts:

For Two Sum, we have the solution of O(n) using a HashSet.
For this one, because the array is already sorted, it becomes quite easy using two pointer, left and right

### Solutions:

```java
public class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int left = 0, right = numbers.length - 1;
        int[] result = new int[2];
        while (left < right) {
            int tmp = numbers[left] + numbers[right];
            if (tmp == target) {
                result[0] = left + 1;
                result[1] = right + 1;
                break;
            }
            if (tmp > target) {
                right --;
            }
            else {
                left ++;
            }
        }
        return result;
    }
}
```