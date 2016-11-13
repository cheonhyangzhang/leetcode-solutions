# 90 Subsets II – Medium


### Problem:



Given a collection of integers that might contain duplicates, nums, return all possible subsets.

Note:

Elements in a subset must be in non-descending order.
The solution set must not contain duplicate subsets.
For example,
If nums = [1,2,2], a solution is:

[
  [2],
  [1],
  [1,2,2],
  [2,2],
  [1,2],
  []
]

### Thoughts:



To meet requirement non-descending order, we have to sort the array first.

The difference compared to the version I is that now we have duplicates. So that one more condition is needed to avoid duplicates.


### Solutions:

non-recursion version:

```java
public class Solution {
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        if (nums == null)
            return null;
        Arrays.sort(nums);
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        result.add(new ArrayList<Integer>());
        List<List<Integer>> toAddAll = new ArrayList<List<Integer>>();
        HashSet<List<Integer>> helper = new HashSet<List<Integer>>();
        for (int i = 0; i < nums.length; i++){ //get sets that are already in result toAddAll.clear(); if (i > 0 && nums[i] == nums[i-1]){
                for (List<Integer> a : result){
                    if (helper.contains(a) == true){
                        List<Integer> toAdd = new ArrayList<Integer>(a);
                        toAdd.add(nums[i]);
                        toAddAll.add(toAdd);
                        helper.add(toAdd);
                        helper.remove(a);
                    }
                }
            }//if i > 0
            else{
                helper.clear();
                for (List<Integer> a : result){
                    List<Integer> toAdd = new ArrayList<Integer>(a);
                    toAdd.add(nums[i]);
                    toAddAll.add(toAdd);
                    helper.add(toAdd);
                }
            }//else
            result.addAll(toAddAll);
        }//for i
        //add empty set
        return result;
    }
}
```
Updated: 11/10/2016 
Improved logic.
Recursion version:

```java
public class Solution {
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        List<List<Integer>> result = new LinkedList<List<Integer>>();
        if (nums == null || nums.length == 0) {
            return result;
        }
        Arrays.sort(nums);
        process(result, new LinkedList<Integer>(), 0, nums);
        return result;
    }
    private void process(List<List<Integer>> result, List<Integer> curr, int start, int[] nums) {
        result.add(new LinkedList<Integer>(curr));
        for (int i = start; i < nums.length; i ++) {
            if (i == start || nums[i] != nums[i-1]){
                curr.add(nums[i]);
                process(result, curr, i + 1, nums);
                curr.remove(curr.size() - 1);
            }
        }
    }
}
```
