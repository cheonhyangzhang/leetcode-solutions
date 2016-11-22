# 118 Pascal’s Triangle – Easy


### Problem:



Given numRows, generate the first numRows of Pascal’s triangle.

For example, given numRows = 5,
Return

[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]

### Thoughts:


Very straight forward based on formula of Pascal’s Triangle.


### Solutions:


```java
public class Solution {
    public List<List<Integer>> generate(int numRows) {
        List<List<Integer>> result = new LinkedList<List<Integer>>();
        for (int i = 0; i < numRows; i ++) {
            List<Integer> toAdd = new ArrayList<Integer>();
            for (int j = 0; j < i + 1; j ++) {
                if (j == 0 || j == i) {
                    toAdd.add(1);
                }
                else {
                    List<Integer> previous = result.get(i-1);
                    toAdd.add(previous.get(j - 1) + previous.get(j));
                }
            }
            result.add(toAdd);
        }
        return result;
    }
}
```