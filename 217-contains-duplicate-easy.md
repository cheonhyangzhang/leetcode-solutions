# 217 Contains Duplicate – Easy

### Problem:
Given an array of integers, find if the array contains any duplicates. Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct.

### Thoughts:
This is too straight forward and simple. I am curious if there is a solution that only takes O(1) space.

From running time perspective, we have to touch every element at lease once, so it needs to be O(n).

### Solutions:

```java
public class Solution {
    public boolean containsDuplicate(int[] nums) {
        HashSet<Integer> set = new HashSet<Integer>();
        for (int i = 0; i < nums.length; i ++){
            if (set.contains(nums[i])){
                return true;
            }
            set.add(nums[i]);
        }    
        return false;
    }
}
```