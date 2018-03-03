# 46  Permutations – Medium


### Problem:



Given a collection of numbers, return all possible permutations.

For example,
[1,2,3] have the following permutations:
[1,2,3], [1,3,2], [2,1,3], [2,3,1], [3,1,2], and [3,2,1].

### Thoughts:



It could be solved using modified DFS.  Each time insert one element that has not been inserted yet.

The idea it so start with empty set. Each time , one number is introduced, for each existing solution, insert this number to all possible positions. This is the non-DFS version solution.


### Solutions:



DFS:

```java
class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> res = new LinkedList<>();
        boolean[] visited = new boolean[nums.length];
        dfs(nums, res, new LinkedList<Integer>(), visited);
        return res;
    }
    private void dfs(int[] nums, List<List<Integer>> res, List<Integer> curr, boolean[] visited) {
        if (curr.size() == nums.length) {
            res.add(new LinkedList<Integer>(curr));
            return;
        }
        for (int i = 0; i < nums.length; i ++) {
            if (visited[i] == false) {
                visited[i] = true;
                curr.add(nums[i]);
                dfs(nums, res, curr, visited);
                curr.remove(curr.size() - 1);
                visited[i] = false;
            }
        }
    }
}
```
Non-DFS version:

```java
public class Solution {
    public List<List<Integer>> permute(int[] num) {
        List<List<Integer>> result = new ArrayList<List<Integer>>();
 
        //start from an empty list
        result.add(new ArrayList<Integer>());
        List<List<Integer>> current = new ArrayList<List<Integer>>();
        for (int i = 0; i < num.length; i++) {
            //list of list in current iteration of the array num
            current.clear();
            for (List<Integer> l : result) {
            // # of locations to insert is largest index + 1
                for (int j = 0; j < l.size()+1; j++) {
                    // + add num[i] to different locations
                    l.add(j, num[i]);
                    ArrayList<Integer> temp = new ArrayList<Integer>(l);
                    current.add(temp);
                    l.remove(j); 
                }
            }
        result = new ArrayList<List<Integer>>(current);
        }
        return result;
    }
}
```