# 268 Missing Number - Medium

### Problem:

Given an array containing n distinct numbers taken from 0, 1, 2, ..., n, find the one that is missing from the array.

For example,
Given nums = [0, 1, 3] return 2.

Note:
Your algorithm should run in linear runtime complexity. Could you implement it using only constant extra space complexity?

### Solutions:

```java
public class Solution {
    public int missingNumber(int[] nums) {
        boolean[] app = new boolean[nums.length + 1];
        for (int i = 0; i < nums.length; i ++) {
            app[nums[i]] = true;
        }
        for (int i = 0; i < app.length; i ++) {
            if (!app[i]) {
                return i;
            }
        }
        return 0;
    }
}
```

```java
public class Solution {
    public int missingNumber(int[] nums) {
        int i = 0;
        while ( i < nums.length) {
            //if nums[i] == n ?
            if (nums[i] == nums.length) {
                i ++;
                continue;
            }
            if (nums[i] != i) {
                int tmp = nums[i];
                nums[i] = nums[nums[i]];
                nums[tmp] = tmp;
            }   
            else {
                i ++;
            }
        }
        for (int j = 0; j < nums.length; j ++) {
            if (nums[j] != j) {
                return j;
            }
        }
        return nums.length;
    }
}
```

```java
public class Solution {
    public int missingNumber(int[] nums) {
        int sum = 0;
        int expected = (1 + nums.length) * nums.length / 2;
        for (int i = 0; i < nums.length; i ++) {
            sum += nums[i];
        }
        return expected - sum;
    }
}
```

```java
public class Solution {
    public int missingNumber(int[] nums) {
        int miss = 0;
        for (int i = 0; i < nums.length; i ++) {
            miss = miss ^ i + 1;
            miss = miss ^ nums[i];
        }
        return miss;
    }
}
```