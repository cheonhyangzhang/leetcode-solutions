# 119 Pascal’s Triangle II – Medium


### Problem:



Given an index k, return the kth row of the Pascal’s triangle.

For example, given k = 3,
Return [1,3,3,1].

Note:
Could you optimize your algorithm to use only O(k) extra space?


### Thoughts:



Similar to the Version I. Actually, this problem could be solved using the Version I solution, instead of returning the whole triangle, return the kth row.

But it could be optimized  to use only O(k) space. Only use on array then all calculations will be using this single array. Each time when calculating element in a new row, calculate from the right to left so that we don’t overwrite any existing elements in the array.


### Solutions:


```java
public class Solution {
    public List<Integer> getRow(int rowIndex) {
        List<Integer> result = new ArrayList<Integer>();
        for (int i = 0;i < rowIndex + 1; i ++) {
            result.add(1);
            for (int j = i; j >=0; j --) {
                if (j != 0 && j != i) {
                    result.set(j, result.get(j) + result.get(j-1));
                }
            } 
        }
        return result;
    }
}
```