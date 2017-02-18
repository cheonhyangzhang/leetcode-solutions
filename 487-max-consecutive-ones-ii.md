# 487 Max Consecutive Ones II

### Problem:

Given a binary array, find the maximum number of consecutive 1s in this array if you can flip at most one 0.

Example 1:
```
Input: [1,0,1,1,0]
Output: 4
Explanation: Flip the first zero will get the the maximum number of consecutive 1s.
    After flipping, the maximum number of consecutive 1s is 4.
```

Note:

1. The input array will only contain 0 and 1.
2. The length of input array is a positive integer and will not exceed 10,000

Follow up:
What if the input numbers come in one by one as an infinite stream? In other words, you can't store all numbers coming from the stream as it's too large to hold in memory. Could you solve it efficiently?

### Solutions:

```java
public class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {
        int[] count = new int[2];
        int index = 0;
        int max = 0;
        boolean zero = false;
        for (int i = 0; i < nums.length; i ++) {
            if (nums[i] == 1) {
                count[index] ++;
                max = Math.max(max, count[0] + count[1]);
            }
            else {
                zero = true;
                index = index ^ 1;
                count[index] = 0;
            }
        }
        if (zero == true) {
            max ++;
        }
        return max;
    }
}
```