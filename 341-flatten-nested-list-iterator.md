# 341 Flatten Nested List Iterator

### Problem:

Given a nested list of integers, implement an iterator to flatten it.

Each element is either an integer, or a list -- whose elements may also be integers or other lists.

Example 1:
Given the list [[1,1],2,[1,1]],

By calling next repeatedly until hasNext returns false, the order of elements returned by next should be: [1,1,2,1,1].

Example 2:
Given the list [1,[4,[6]]],

By calling next repeatedly until hasNext returns false, the order of elements returned by next should be: [1,4,6].

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
public class NestedIterator implements Iterator<Integer> {

    private Stack<Iterator<NestedInteger>> s = new Stack<Iterator<NestedInteger>>();
    private Integer next = null;
    public NestedIterator(List<NestedInteger> nestedList) {
        Iterator<NestedInteger> it = nestedList.iterator();
        s.push(it);
        findNext();
    }
    private void findNext() {
        next = null;
        Iterator<NestedInteger> it = null;
        while (!s.isEmpty()) {
            it = s.peek();
            if (!it.hasNext()) {
                s.pop();
                continue;
            }
            NestedInteger ni = it.next();
            if (ni.isInteger()) {
                next = ni.getInteger();
                break;
            }
            else {
                s.push(ni.getList().iterator());
            }
        }
    }
    @Override
    public Integer next() {
        Integer result = next;
        findNext();
        return result;
    }

    @Override
    public boolean hasNext() {
        return next != null;
    }
}

/**
 * Your NestedIterator object will be instantiated and called as such:
 * NestedIterator i = new NestedIterator(nestedList);
 * while (i.hasNext()) v[f()] = i.next();
 */
```