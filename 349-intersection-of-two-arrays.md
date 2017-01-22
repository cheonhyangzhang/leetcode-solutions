# 349 Intersection of Two Arrays

### Problem:

Given two arrays, write a function to compute their intersection.

Example:
Given nums1 = [1, 2, 2, 1], nums2 = [2, 2], return [2].

Note:
Each element in the result must be unique.
The result can be in any order.
Show Company Tags
Show Tags
Show Similar Problems


### Solutions:

```java
public class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        HashSet<Integer> app = new HashSet<Integer>();
        for (int i = 0; i < nums1.length; i ++) {
            app.add(nums1[i]);
        }
        HashSet<Integer> res = new HashSet<Integer>();
        for (int i = 0; i < nums2.length; i ++) {
            if (app.contains(nums2[i])) {
                res.add(nums2[i]);
            }
        }
        int[] result = new int[res.size()];
        int i = 0;
        for (Integer j:res) {
            result[i++] = j;
        }
        return result;
    }
}
```