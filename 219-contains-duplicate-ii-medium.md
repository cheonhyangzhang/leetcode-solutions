# 219 Contains Duplicate II – Medium


### Problem:
Given an array of integers and an integer k, find out whether there are two distinct indices i and j in the array such that nums[i] = nums[j] and the difference between i and j is at most k.

### Thoughts:
This is similar to version I. The difference is that instead of only test if there is duplicate, we need to tell the difference of two indices of the duplicate values.

And we care about the smallest difference.

Notice that you need to put value, index pair into the hashmap no matter if that element already appeared.

### Solutions:

```java
public class Solution {
    public boolean containsNearbyDuplicate(int[] nums, int k) {
        HashMap<Integer, Integer> left = new HashMap<Integer, Integer>();
        for (int i = 0; i < nums.length; i ++){
            if (left.containsKey(nums[i])){
                if (i - left.get(nums[i])<= k){
                    return true;
                }
            }
            left.put(nums[i], i);
        }//for i
        return false;
    }
}
```