# 307. Range Sum Query - Mutable

### Problem:

<pre>
Given an integer array nums, find the sum of the elements between indices i and j (i ≤ j), inclusive.

The update(i, val) function modifies nums by updating the element at index i to val.
Example:
Given nums = [1, 3, 5]

sumRange(0, 2) -> 9
update(1, 2)
sumRange(0, 2) -> 8
Note:
The array is only modifiable by the update function.
You may assume the number of calls to update and sumRange function is distributed evenly.
</pre>

https://en.wikipedia.org/wiki/Fenwick_tree

### Solutions:

```java
public class NumArray {
    private int[] sums;
    private int[] nums;
    public NumArray(int[] nums) {
        this.nums = nums;
        sums = new int[nums.length];
        int sum = 0;
        for (int i = 0; i < nums.length; i ++) {
            sum += nums[i];
            sums[i] = sum;
        }
    }

    void update(int i, int val) {
        int diff = val - nums[i];
        nums[i] = val;
        for (int x = i; x < nums.length; x ++) {
            sums[x] += diff;
        }
    }

    public int sumRange(int i, int j) {
        return sums[j] - sums[i] + nums[i];
    }
}


// Your NumArray object will be instantiated and called as such:
// NumArray numArray = new NumArray(nums);
// numArray.sumRange(0, 1);
// numArray.update(1, 10);
// numArray.sumRange(1, 2);
```

```java
public class NumArray {
    int[] sums;
    int[] nums;
    public NumArray(int[] nums) {
        sums = new int[nums.length + 1];
        this.nums = new int[nums.length];
        for (int i = 0; i < nums.length; i ++) {
            update(i, nums[i]);
        }
    }
    
    public void update(int i, int val) {
        int diff = val - nums[i];
        int j = i + 1;
        while (j < sums.length) {
            sums[j] += diff;
            j = j + (j&(-j));
        }
        nums[i] = val;
    }
    private int getSum(int i) {
        int sum = 0;
        while (i > 0) {
            sum += sums[i];
            i = i - (i&(-i));
        }
        return sum;
    }
    
    public int sumRange(int i, int j) {
        return getSum(j + 1) - getSum(i);
    }
}

/**
 * Your NumArray object will be instantiated and called as such:
 * NumArray obj = new NumArray(nums);
 * obj.update(i,val);
 * int param_2 = obj.sumRange(i,j);
 */
```