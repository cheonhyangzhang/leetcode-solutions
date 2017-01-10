# 254 Factor Combinations - Medium

### Problem:
<pre>
Numbers can be regarded as product of its factors. For example,

8 = 2 x 2 x 2;
  = 2 x 4.
  
Write a function that takes an integer n and return all possible combinations of its factors.

Note: 
You may assume that n is always positive.
Factors should be greater than 1 and less than n.

Examples: 
input: 1
output: 
[]
input: 37
output: 
[]
input: 12
output:
  [
    [2, 6],
    [2, 2, 3],
    [3, 4]
  ]  
input: 32
output:
[
  [2, 16],
  [2, 2, 8],
  [2, 2, 2, 4],
  [2, 2, 2, 2, 2],
  [2, 4, 4],
  [4, 8]
]
</pre>

# Solutions:

```java
public class Solution {
    public List<List<Integer>> getFactors(int n) {
        List<List<Integer>> result = new LinkedList<List<Integer>>();
        process(2, result, new LinkedList<Integer>(), n);
        return result;
    }
    private void process(int start, List<List<Integer>> result, List<Integer> curr, int n) {
        if (n == 1) {
            if (curr.size() > 1) {
                result.add(new LinkedList<Integer>(curr));
            }
        }
        for (int i = start; i <= n; i ++) {
            if (n % i == 0) {
                curr.add(i);
                process(i, result, curr, n / i);
                curr.remove(curr.size() - 1);
            }
        }
    }
}
```