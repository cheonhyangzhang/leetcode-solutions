# 47  Permutations II – Medium


### Problem:



Given a collection of numbers that might contain duplicates, return all possible unique permutations.

For example,
[1,1,2] have the following unique permutations:
[1,1,2], [1,2,1], and [2,1,1].


### Thoughts:



This is similar to Permutations, the only difference is that the collection might contain duplicates.

So the modification is to avoid duplicate solution.

So the add condition is that for any duplicate elements, you only want to add it if the previous one ( duplicate) is added.

Say for 0 1 1, for the second 1, only insert it if the previous 1 is inserted so that we could avoid have two 0 1 1 permutation and 0 1 1 permutation.


### Solutions:

```java
class Solution {
    public List<List<Integer>> permuteUnique(int[] nums) {
        List<List<Integer>> res = new LinkedList<>();
        if (nums == null || nums.length == 0) {
            return res;
        }
        Arrays.sort(nums);
        boolean[] visited = new boolean[nums.length];
        dfs(nums, visited, new LinkedList<Integer>(), res);
        return res;
    }
    private void dfs(int[] nums, boolean[] visited, List<Integer> curr, List<List<Integer>> res) {
        if (curr.size() == nums.length) {
            res.add(new LinkedList<Integer>(curr));
            return;
        }
        for (int i = 0; i < nums.length; i ++) {
            if (visited[i] == true) {
                continue;
            }
            if (i == 0 || nums[i] != nums[i - 1] || (nums[i] == nums[i - 1] && visited[i - 1] == true)) {
                visited[i] = true;
                curr.add(nums[i]);
                dfs(nums, visited, curr, res);
                curr.remove(curr.size() - 1);
                visited[i] = false;
            }
        }
    }
}
```