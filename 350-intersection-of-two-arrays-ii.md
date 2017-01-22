# 350 Intersection of Two Arrays II

### Problem:

<pre>
Given two arrays, write a function to compute their intersection.

Example:
Given nums1 = [1, 2, 2, 1], nums2 = [2, 2], return [2, 2].

Note:
Each element in the result should appear as many times as it shows in both arrays.
The result can be in any order.
Follow up:
What if the given array is already sorted? How would you optimize your algorithm?
What if nums1's size is small compared to nums2's size? Which algorithm is better?
What if elements of nums2 are stored on disk, and the memory is limited such that you cannot load all elements into the memory at once?
Show Tags
Show Similar Problems

</pre>

### Solutions:

```java
public class Solution {
    public int[] intersect(int[] nums1, int[] nums2) {
        HashMap<Integer, Integer> data = new HashMap<Integer, Integer>();
        for (int i = 0; i < nums1.length; i ++){
            if (!data.containsKey(nums1[i])) {
                data.put(nums1[i], 1);
            }
            else {
                data.put(nums1[i], data.get(nums1[i]) + 1);
            }
        }
        List<Integer> res = new LinkedList<Integer>();
        for (int i = 0; i < nums2.length; i ++) {
            if (data.containsKey(nums2[i]) && data.get(nums2[i]) != 0) {
                res.add(nums2[i]);
                data.put(nums2[i], data.get(nums2[i]) - 1);
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