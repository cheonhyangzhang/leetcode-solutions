# 216 Combination Sum III – Medium


### Problem:
Find all possible combinations of k numbers that add up to a number n, given that only numbers from 1 to 9 can be used and each combination should be a unique set of numbers.

Ensure that numbers within the set are sorted in ascending order.

Example 1:Input: k = 3, n = 7
Output:
```
[[1,2,4]]
```
Example 2:

Input: k = 3, n = 9

Output:
```
[[1,2,6], [1,3,5], [2,3,4]]
```

### Thoughts:
This problem is modified based the Combination Sum II.

Difference is:

Candidates are numbers from 1 – 9 instead of given array.

Secondly, there is no constraints on number of elements in version II, but in III, the list of elements that adds up to given target value n has to have exact k elements.

Below is using an approach that’s modified based on the solution to Version II.

### Solutions:

```java
public class Solution {
    public List<List<Integer>> combinationSum3(int k, int n) {
        List<List<Integer>> result = new LinkedList<List<Integer>>();
        if (k > 9 || n > 45) {
            return result;
        }
        dfs(result, k, n, new LinkedList<Integer>(), 1);
        return result;
    }
    private void dfs(List<List<Integer>> result, int k, int n, List<Integer> curr, int start) {
        if (k == 0) {
            if (n == 0) {
                result.add(new LinkedList<Integer>(curr));
            }
            return;
        }
        for (int i = start; i <= 9; i ++) {
            if ((9 - i) < k - 1) {
                return;
            }
            curr.add(i);
            dfs(result, k - 1, n - i, curr, i + 1);
            curr.remove(curr.size() - 1);
        }
    }
}
```