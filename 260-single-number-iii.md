# 260. Single Number III

### Problem:

 My Submissions
Total Accepted: 56553
Total Submissions: 115017
Difficulty: Medium
Contributors: Admin
Given an array of numbers nums, in which exactly two elements appear only once and all the other elements appear exactly twice. Find the two elements that appear only once.

For example:

Given nums = [1, 2, 1, 3, 2, 5], return [3, 5].

Note:
The order of the result is not important. So in the above example, [5, 3] is also correct.
Your algorithm should run in linear runtime complexity. Could you implement it using only constant space complexity?

### Solutions:

```java
public class Solution {
    public int[] singleNumber(int[] nums) {
        HashSet<Integer> app = new HashSet<Integer>();
        for (int i = 0; i < nums.length; i ++) {
            if (app.contains(nums[i])) {
                app.remove(nums[i]);
            }
            else {
                app.add(nums[i]);
            }
        }
        int[] result = new int[2];
        Iterator<Integer> it = app.iterator();
        result[0] = it.next();
        result[1] = it.next();
        return result;
    }
}
```
