# 339 Nested List Weight Sum

### Problem:

Given a nested list of integers, return the sum of all integers in the list weighted by their depth.

Each element is either an integer, or a list -- whose elements may also be integers or other lists.

Example 1:
Given the list [[1,1],2,[1,1]], return 10. (four 1's at depth 2, one 2 at depth 1)

Example 2:
Given the list [1,[4,[6]]], return 27. (one 1 at depth 1, one 4 at depth 2, and one 6 at depth 3; 1 + 4 \* 2 + 6 \* 3 = 27)

### Solutions:

```java
/**
 * // This is the interface that allows for creating nested lists.
 * // You should not implement it, or speculate about its implementation
 * public interface NestedInteger {
 *
 *     // @return true if this NestedInteger holds a single integer, rather than a nested list.
 *     public boolean isInteger();
 *
 *     // @return the single integer that this NestedInteger holds, if it holds a single integer
 *     // Return null if this NestedInteger holds a nested list
 *     public Integer getInteger();
 *
 *     // @return the nested list that this NestedInteger holds, if it holds a nested list
 *     // Return null if this NestedInteger holds a single integer
 *     public List<NestedInteger> getList();
 * }
 */
public class Solution {
    public int depthSum(List<NestedInteger> nestedList) {
        return ds(1, nestedList);
    }
    private int ds(int level, List<NestedInteger> nestedList) {
        int sum = 0;
        for (NestedInteger ni:nestedList) {
            if (ni.isInteger()) {
                sum +=level * ni.getInteger();
            }
            else {
                sum +=ds(level + 1, ni.getList());
            }
        }
        return sum;
    }
}
```

```java
/**
 * // This is the interface that allows for creating nested lists.
 * // You should not implement it, or speculate about its implementation
 * public interface NestedInteger {
 *     // Constructor initializes an empty nested list.
 *     public NestedInteger();
 *
 *     // Constructor initializes a single integer.
 *     public NestedInteger(int value);
 *
 *     // @return true if this NestedInteger holds a single integer, rather than a nested list.
 *     public boolean isInteger();
 *
 *     // @return the single integer that this NestedInteger holds, if it holds a single integer
 *     // Return null if this NestedInteger holds a nested list
 *     public Integer getInteger();
 *
 *     // Set this NestedInteger to hold a single integer.
 *     public void setInteger(int value);
 *
 *     // Set this NestedInteger to hold a nested list and adds a nested integer to it.
 *     public void add(NestedInteger ni);
 *
 *     // @return the nested list that this NestedInteger holds, if it holds a nested list
 *     // Return null if this NestedInteger holds a single integer
 *     public List<NestedInteger> getList();
 * }
 */
class Solution {
    public int depthSum(List<NestedInteger> nestedList) {
        Queue<NestedInteger> q = new LinkedList<>();
        Queue<Integer> w = new LinkedList<>();
        for (NestedInteger ni:nestedList) {
            q.add(ni);
            w.add(1);
        }
        int count = 0;
        while (!q.isEmpty()) {
            NestedInteger ni = q.poll();
            int weight = w.poll();
            if (ni.isInteger()) {
                count += ni.getInteger() * weight;
                continue;
            }
            for (NestedInteger n:ni.getList()) {
                q.add(n);
                w.add(weight + 1);
            }
        }
        return count;
    }
}
```