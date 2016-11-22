# 78 Subsets – Medium


### Problem:



Given a set of distinct integers, nums, return all possible subsets.

Note:

Elements in a subset must be in non-descending order.
The solution set must not contain duplicate subsets.
For example,
If nums = [1,2,3], a solution is:

[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]

### Thoughts:



Init solution set with empty list.

Iterating over all numbers, for each number, add it to all existing subsets, but keep the existing subests.

Say for numbers [1, 2, 3],

Init solution set to be []

1: [],    [1]

2: [],[1]    [2],[1,2]

3: [],[1],[2],[1,2]   [3],[1,3],[2,3],[1,2,3]


### Solutions:



```java
public class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        if (nums == null)
            return null;
        Arrays.sort(nums);
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        result.add(new ArrayList<Integer>());
        List<List<Integer>> toAddAll = new ArrayList<List<Integer>>();
        for (int i = 0; i < nums.length; i++) {
            toAddAll.clear();
            //get sets that are already in result
            for (List<Integer> a : result) {
                List<Integer> toAdd = new ArrayList<Integer>(a);
                toAdd.add(nums[i]);
                toAddAll.add(toAdd);
            }
            result.addAll(toAddAll);
        }
        //add empty set
        return result;
    }
}
```
Recursion version:

```java
public class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> result = new LinkedList<List<Integer>>();
        Arrays.sort(nums);
        process(0, nums, result, new LinkedList<Integer>());
        return result;
    }
    private void process(int start, int[] nums, List<List<Integer>> result, List<Integer> curr) {
        result.add(new LinkedList<Integer>(curr));
        for (int i = start; i < nums.length; i ++) {
            curr.add(nums[i]);
            process(i+1, nums, result, curr);
            curr.remove(curr.size() - 1);
        }
    }
}
```