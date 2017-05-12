# 220 LeetCode Java: Contains Duplicate III – Medium


### Problem:
Given an array of integers, find out whether there are two distinct indices i and j in the array such that the difference between nums[i] andnums[j] is at most t and the difference between i and j is at most k.

### Thoughts:
This is a very difficult one if you don’t know there is a class called TreeSet.

With the help of TreeSet, it just becomes super easy.

A TreeSet is keeping all elements in k range based on current index.

Alternative solution is to use a HashMap to keep the index for an element.

### Solutions:

```java
public class Solution {
    public boolean containsNearbyAlmostDuplicate(int[] nums, int k, int t) {
        if (k < 1 || t < 0)
            return false;
        SortedSet<Long> set = new TreeSet<Long>();
        for (int i = 0; i < nums.length; i++) {
            long left = (long) nums[i] - t;
            long right = (long) nums[i] + t + 1;
            SortedSet<Long> subSet = set.subSet(left, right);
            if (!subSet.isEmpty())
                return true;
            set.add((long) nums[i]);
            if (i >= k) {
                set.remove((long) nums[i - k]);
            }
        }
        return false;
    }
}
```

···java
public class Solution {
    public boolean containsNearbyAlmostDuplicate(int[] nums, int k, int t) {
        HashMap<Integer, LinkedList<Integer>> index = new HashMap<Integer, LinkedList<Integer>>();
        for (int i = 0; i < nums.length; i ++) {
            if (!index.containsKey(nums[i])) {
                index.put(nums[i], new LinkedList<Integer>());
            }
            index.get(nums[i]).add(i);
        }
        Arrays.sort(nums);
        for (int i = 0; i < nums.length - 1; i ++) {
            for (int j = i + 1; j < nums.length; j ++) {
                int diff = nums[j] - nums[i];
                if (diff >= 0 && diff <=t) {
                    for (Integer a:index.get(nums[j])) {
                        for (Integer b:index.get(nums[i])) {
                            if (a!=b && Math.abs(a-b) <= k ) {
                                return true;
                            }
                        }
                    }
                }
                else {
                    break;
                }
            }
        }
        return false;
    }
}
```