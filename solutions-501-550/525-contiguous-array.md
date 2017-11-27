# 525 Contiguous Array

Given a binary array, find the maximum length of a contiguous subarray with equal number of 0 and 1.

Example 1:
```
Input: [0,1]
Output: 2
```
Explanation: [0, 1] is the longest contiguous subarray with equal number of 0 and 1.
Example 2:
```
Input: [0,1,0]
Output: 2
```
Explanation: [0, 1] (or [1, 0]) is a longest contiguous subarray with equal number of 0 and 1.
Note: The length of the given binary array will not exceed 50,000.

### Solutions

```java
class Solution {
    public int findMaxLength(int[] nums) {
        int res = 0, sum = 0;
        HashMap<Integer, Integer> index = new HashMap<Integer, Integer>();
        index.put(0, -1);
        for (int i = 0; i < nums.length; i ++) {
            if (nums[i] == 1) {
                sum ++;
            }
            else {
                sum --;
            }
            if (index.containsKey(sum)) {
                res = Math.max(res, i - index.get(sum));
            } else {
                index.put(sum, i);
            }
        }
        return res;
    }
}
```