# 506 Relative Ranks

### Problem:

Given scores of N athletes, find their relative ranks and the people with the top three highest scores, who will be awarded medals: "Gold Medal", "Silver Medal" and "Bronze Medal".

Example 1:
```
Input: [5, 4, 3, 2, 1]
Output: ["Gold Medal", "Silver Medal", "Bronze Medal", "4", "5"]
Explanation: The first three athletes got the top three highest scores, so they got "Gold Medal", "Silver Medal" and "Bronze Medal". 
For the left two athletes, you just need to output their relative ranks according to their scores.
```
Note:
1. N is a positive integer and won't exceed 10,000.
2. All the scores of athletes are guaranteed to be unique.

### Solutions:

```java
public class Solution {
    public String[] findRelativeRanks(int[] nums) {
        if (nums == null) {
            return null;
        }
        String[] result = new String[nums.length];
        HashMap<Integer, Integer> index = new HashMap<Integer, Integer>();
        for (int i = 0; i < nums.length; i ++) {
            index.put(nums[i], i);
        }
        Arrays.sort(nums);
        String[] prizes = new String[]{"Gold Medal", "Silver Medal", "Bronze Medal"};
        for (int i = nums.length - 1; i >= 0; i --) {
            int rank = nums.length - 1 - i;
            if (rank < 3) {
                result[index.get(nums[i])] = prizes[rank];
            }
            else {
                result[index.get(nums[i])] = "" + (rank + 1);
            }
        }
        return result;
    }
}
```