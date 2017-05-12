# 229 Majority Element II – Medium

### Problem:
Given an integer array of size n, find all elements that appear more than ⌊ n/3 ⌋ times. The algorithm should run in linear time and in O(1) space.

### Thoughts:
This is similar to Majority Element I. It’s always easy to come up with Time O(n) and Space O(n) solution with the help of HashMap, however, the problem requires O(1) space which makes it a little harder.

In version I, a counter is used to find out the major element. Because that’s element appears more than n/2, so the major element will eventually stay after iterating.

For this problem, we need to find the element that appears more than n/3, it’s easy to know that there could be at most two such element. So we will need 2 candidate variables and 2 counters.

Since each counter is not keeping the total count of appear, after iterating the array, we need to re-calculate the count for the two candidates to determine if they are actually the majority elements.

### Solutions:

```java
public class Solution {
    public List<Integer> majorityElement(int[] nums) {
        Integer cand1 = null, cand2 = null;
        int count1 = 0, count2 = 0;
        for (int i = 0; i < nums.length; i ++) {
            if (cand1 != null && cand1 == nums[i]) {
                count1 ++;
            }
            else if (cand2 !=null && cand2 == nums[i]) {
                count2 ++;
            }
            else if (count1 == 0) {
                cand1 = nums[i];
                count1 ++;
            }
            else if (count2 == 0) {
                cand2 = nums[i];
                count2 ++;
            }
            else {
                count1 --;
                count2 --;
            }
        }
        List<Integer> result = new LinkedList<Integer>();
        count1 = 0;
        count2 = 0;
        for (int i = 0; i < nums.length; i ++) {
            if (cand1 != null && nums[i] == cand1) {
                count1 ++;
            }
            if (cand2 != null && nums[i] == cand2) {
                count2 ++;
            }
        }
        if (count1 > nums.length / 3) {
            result.add(cand1);
        }
        if (count2 > nums.length / 3) {
            result.add(cand2);
        }
        return result;
    }
}
```