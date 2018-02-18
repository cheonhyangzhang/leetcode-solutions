# 228 Summary Ranges – Medium

### Problem:
Given a sorted integer array without duplicates, return the summary of its ranges.

For example, given [0,1,2,4,5,7], return [“0->2″,”4->5″,”7”].

### Thoughts:
This problem is similar to the missing ranges but this one is easier because there is no trouble of Integer Overflow problem.

In my solution, I use two for loop nested but actually it’s only O(n) time. Because i is skipping the index that j has visited.

So it can be done by using only one loop.

### Solutions:

```java
public class Solution {
    public List<String> summaryRanges(int[] nums) {
        List<String> result = new LinkedList<String>();
        if (nums == null || nums.length == 0) {
            return result;
        }
        for (int i = 0; i < nums.length; i ++) {
            if (i == nums.length - 1 || nums[i] != nums[i + 1] - 1) {
                result.add(nums[i] + "");
                continue;
            }
            int left = nums[i];
            int j = i + 1;
            for (; j < nums.length; j ++) {
                if (j == nums.length - 1 || nums[j] != nums[j + 1] - 1) {
                    break;
                }
            }
            result.add(left + "->" + nums[j]);
            i = j;
        }
        return result;
    }
}
```

```java
class Solution {
    public List<String> summaryRanges(int[] nums) {
        List<String> res = new LinkedList<String>();
        if (nums.length == 0) {
            return res;
        }
        int start = -1;
        int end = -1;
        for (int i = 0; i < nums.length; i ++) {
            if (i == 0) {
                start = nums[i];
                end = nums[i];
            }
            else {
                if (nums[i] == end + 1) {
                    end = nums[i];
                }
                else {
                    process(res, start, end);
                    start = nums[i];
                    end = nums[i];
                }
            }
        }
        process(res, start, end);
        return res;
    }
    private void process(List<String> res, int start, int end) {
        if (start == end) {
            res.add(start + "");
        }
        else {
            res.add(start + "->" + end);
        }
    }
}
```