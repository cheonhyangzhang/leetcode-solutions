# 128 Longest Consecutive Sequence

### Problem:

Given an unsorted array of integers, find the length of the longest consecutive elements sequence.

For example,
Given [100, 4, 200, 1, 3, 2],
The longest consecutive elements sequence is [1, 2, 3, 4]. Return its length: 4.

Your algorithm should run in O(n) complexity.

### Solutions:

```java
public class Solution {
    public int longestConsecutive(int[] nums) {
        HashMap<Integer, Integer> left = new HashMap<Integer, Integer>();
        HashMap<Integer, Integer> right = new HashMap<Integer, Integer>();
        HashSet<Integer> visited = new HashSet<Integer>();
        int max = 0;
        for (int i = 0; i < nums.length; i ++) {
            if (visited.contains(nums[i])) {
                continue;
            }
            if (!right.containsKey(nums[i] - 1) && !left.containsKey(nums[i] + 1)) {
                left.put(nums[i], nums[i]);
                right.put(nums[i], nums[i]);
                max = Math.max(max, 1);             
                visited.add(nums[i]);
                continue;
            }
            if (right.containsKey(nums[i] - 1) && left.containsKey(nums[i] + 1)) {
                int a = right.get(nums[i] - 1);
                int b = left.get(nums[i] + 1);
                right.remove(nums[i] - 1);
                left.remove(nums[i] + 1);
                left.put(a, b);
                right.put(b, a);
                max = Math.max(max, b - a + 1);
                visited.add(nums[i]);
                continue;
            }
            if (right.containsKey(nums[i] - 1)) {
                int a = right.get(nums[i] - 1);
                int b = nums[i] - 1;
                right.remove(b);
                left.put(a, nums[i]);
                right.put(nums[i], a);
                max = Math.max(max, b - a + 2);
            }
            if (left.containsKey(nums[i] + 1)) {
                int a = nums[i] + 1;
                int b = left.get(nums[i] + 1);
                left.remove(a);
                left.put(nums[i], b);
                right.put(b, nums[i]);
                max = Math.max(max, b - a + 2);
            }
            visited.add(nums[i]);
        }
        return max;
    }
}
```

`