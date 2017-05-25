# 163 Missing Ranges 

### Problem
Given a sorted integer array where the range of elements are in the inclusive range [lower, upper], return its missing ranges.

For example, given [0, 1, 3, 50, 75], lower = 0 and upper = 99, return [“2”, “4->49”, “51->74”, “76->99”].

### Thoughts:
The first thought I had for this problem is to do in a recursive way. One thing need to deal with is about Integer overflow.
Actually, I think it’s good to always keep in mind about Integer overflow when you are adding a Integer.

Because, when using a recursive solution, it uses stack to store the state of the function call. So we might need a iterative way which will save some time and be more efficient.
In the second solution, it’s using a iterative way, but still we need to deal with the integer overflow case.

### Solutions:

```java
public class Solution {
    public List<String> findMissingRanges(int[] nums, int lower, int upper) {
        List<String> result = new LinkedList<String>();
        if (nums.length == 0) {
            findRange(result, lower, upper);
            return result;
        }
        if (nums[0] != Integer.MIN_VALUE) {
            findRange(result, lower, nums[0] - 1);
        }
        for (int i = 0; i < nums.length - 1; i ++) {
            if (nums[i] == nums[i+1]) {
                continue;
            }
            findRange(result, nums[i] + 1, nums[i+1] - 1);
        }
        if (nums[nums.length - 1] != Integer.MAX_VALUE) {
            findRange(result, nums[nums.length - 1] + 1, upper);
        }

        return result;
    }
    private void findRange(List<String> result, int low, int up) {
        if (low > up){
            return;
        }
        if (low == up) {
            result.add((low) + "");
            return;
        }
        result.add(low + "->" + up);
    }
}
```

Iterative:
```java
public class Solution {
    public List<String> findMissingRanges(int[] nums, int lower, int upper) {
        List<String> result = new LinkedList<String>();
        int left = 0, right = 0;
        for (int i = -1; i < nums.length; i ++) {
            if (i >= 0) {
                left = nums[i] + 1;
                if (left == Integer.MIN_VALUE) {
                    continue;
                }
            }
            else {
                left = lower;
            }
            if (i + 1 < nums.length) {
                right = nums[i + 1] - 1;
                if (right == Integer.MAX_VALUE) {
                    continue;
                }
            }
            else{
                right = upper;
            }
            if (left > right) {
                continue;
            }
            if (left == right) {
                result.add(left + "");
                continue;
            }
            result.add(left + "->" + right);
        }
        return result;
    }
}
```
