# 303 Range Sum Query - Immutable

### Problem:

<pre>
Given an integer array nums, find the sum of the elements between indices i and j (i ≤ j), inclusive.

Example:
Given nums = [-2, 0, 3, -5, 2, -1]

sumRange(0, 2) -> 1
sumRange(2, 5) -> -1
sumRange(0, 5) -> -3
Note:
You may assume that the array does not change.
There are many calls to sumRange function.
</pre>

### Solutions:

```java
public class NumArray {
    int[] sums;
    int[] nums;
    public NumArray(int[] nums) {
        this.nums = nums;
        sums = new int[nums.length];
        int sum = 0;
        for (int i = 0; i < nums.length; i ++) {
            sum += nums[i];
            sums[i] = sum;
        }
    }

    public int sumRange(int i, int j) {
        return sums[j] - sums[i] + nums[i];
    }
}


// Your NumArray object will be instantiated and called as such:
// NumArray numArray = new NumArray(nums);
// numArray.sumRange(0, 1);
// numArray.sumRange(1, 2);
```