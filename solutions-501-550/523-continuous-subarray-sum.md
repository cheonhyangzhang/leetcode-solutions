# 523 Continuous Subarray Sum

### Problem

Given a list of non-negative numbers and a target integer k, write a function to check if the array has a continuous subarray of size at least 2 that sums up to the multiple of k, that is, sums up to n*k where n is also an integer.

Example 1:
```
Input: [23, 2, 4, 6, 7],  k=6
Output: True
Explanation: Because [2, 4] is a continuous subarray of size 2 and sums up to 6.
```
Example 2:
```
Input: [23, 2, 6, 4, 7],  k=6
Output: True
Explanation: Because [23, 2, 6, 4, 7] is an continuous subarray of size 5 and sums up to 42.
```
Note:
The length of the array won't exceed 10,000.
You may assume the sum of all the numbers is in the range of a signed 32-bit integer.

### Solutions

```java
class Solution {
    public boolean checkSubarraySum(int[] nums, int k) {
        HashMap<Integer, Integer> remain = new HashMap<Integer, Integer>();
        int sum = 0;
        for (int i = 0; i < nums.length; i ++) {
            sum += nums[i];
            if (k == 0) {
                if (remain.containsKey(sum)) {
                    if (remain.get(sum) != i - 1 || i == 1) {
                        return true;
                    }
                }
                else {
                    remain.put(sum, i);
                }
            }
            else {
                int re = sum % k;
                if (re != 0) {
                    if (remain.containsKey(re)) {
                        if (remain.get(re) != i - 1) {
                            return true;
                        }
                    }
                    else {
                        remain.put(re, i);
                    }
                }   
                else if (i > 0) {
                    return true;
                }
            }
        }
        return false;
    }
}
```