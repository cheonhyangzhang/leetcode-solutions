# 347. Top K Frequent Elements

### Problem:

Given a non-empty array of integers, return the k most frequent elements.

For example,
Given [1,1,1,2,2,3] and k = 2, return [1,2].

Note: 
You may assume k is always valid, 1 ≤ k ≤ number of unique elements.
Your algorithm's time complexity must be better than O(n log n), where n is the array's size.

### Solutions:

```java
public class Solution {
    public List<Integer> topKFrequent(int[] nums, int k) {
        HashMap<Integer, Integer> count = new HashMap<Integer, Integer>();
        for (int i = 0; i < nums.length; i ++) {
            if (!count.containsKey(nums[i])) {
                count.put(nums[i], 0);
            }
            count.put(nums[i], count.get(nums[i]) + 1);
        }
        HashMap<Integer, Queue<Integer>> reverse = new HashMap<Integer, Queue<Integer>>();
        PriorityQueue<Integer> app = new PriorityQueue<Integer>(k, Collections.reverseOrder());
        for (Integer i:count.keySet()) {
            int val = count.get(i);
            app.add(val);
            if (!reverse.containsKey(val)){
                reverse.put(val, new LinkedList());
            }
            reverse.get(val).add(i);
        }
        List<Integer> result = new LinkedList<Integer>();
        for (int i = 0; i < k; i ++) {
            int val = app.poll();
            result.add(reverse.get(val).poll());
        }
        return result;
    }
}
```