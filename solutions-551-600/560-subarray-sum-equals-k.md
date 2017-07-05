# 560. Subarray Sum Equals K

### Problem:
Given an array of integers and an integer k, you need to find the total number of continuous subarrays whose sum equals to k.

Example 1:
```
Input:nums = [1,1,1], k = 2
Output: 2
```

Note:
1. The length of the array is in range [1, 20,000].
2. The range of numbers in the array is [-1000, 1000] and the range of the integer k is [-1e7, 1e7].

### Solutions:

```java
public class Solution {
    public int subarraySum(int[] nums, int k) {
        int[] sums = new int[nums.length + 1];
        int sum = 0;
        for (int i = 0; i < nums.length; i ++) {
            sum += nums[i];
            sums[i + 1] = sum;
        }
        int count = 0;
        for (int i = 0; i < nums.length; i ++) {
            int pre = sums[i];
            for (int j = i; j < nums.length; j ++) {
                int tmp = sums[j + 1] - pre;
                if (tmp == k) {
                    count ++;
                }
            }
        }
        return count;
    }
}
```

```java
public class Solution {
    public int subarraySum(int[] nums, int k) {
        int res = 0, sum = 0;
        HashMap<Integer, Integer> count = new HashMap<Integer, Integer>();
        count.put(0, 1);
        for (int i = 0; i < nums.length; i ++) {
            sum += nums[i];
            if (count.containsKey(sum - k)) {
                res += count.get(sum - k);
            }
            int add = 1;
            if (count.containsKey(sum)) {
                add += count.get(sum);
            }
            count.put(sum, add);
        }
        return res;
    }
}
```