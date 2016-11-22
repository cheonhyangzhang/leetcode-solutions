# 77 Combinations – Medium


### Problem:



Given two integers n and k, return all possible combinations of k numbers out of 1 … n.

For example,
If n = 4 and k = 2, a solution is:

[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]

### Thoughts:



This is a very typical question to use DFS.


### Solutions:



```
public class Solution {
    public List<List<Integer>> combine(int n, int k) {
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        if (n <= 0 || n < k)
            return result;
        ArrayList<Integer> current = new ArrayList<Integer>();
        dfs(n, k, 1, current, result); // because it need to begin from 1
        return result;
    }
    private void dfs(int n, int k, int start, ArrayList<Integer> current,
        List<List<Integer>> res) {
        if (current.size() == k) {
            res.add(new ArrayList<Integer>(current));
            return;
        }
 
        for (int i = start; i <= n; i++) {
            current.add(i);
            dfs(n, k, i + 1, current, res);
            current.remove(current.size() - 1);
        }
    }
}
```