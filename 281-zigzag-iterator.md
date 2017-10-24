# 281. Zigzag Iterator

### Problem:

<pre>
Given two 1d vectors, implement an iterator to return their elements alternately.

For example, given two 1d vectors:

v1 = [1, 2]
v2 = [3, 4, 5, 6]
By calling next repeatedly until hasNext returns false, the order of elements returned by next should be: [1, 3, 2, 4, 5, 6].

Follow up: What if you are given k 1d vectors? How well can your code be extended to such cases?

Clarification for the follow up question - Update (2015-09-18):
The "Zigzag" order is not clearly defined and is ambiguous for k > 2 cases. If "Zigzag" does not look right to you, replace "Zigzag" with "Cyclic". For example, given the following input:

[1,2,3]
[4,5,6,7]
[8,9]
It should return [1,4,8,2,5,9,3,6,7].
</pre>

### Solutions:

```java
public class ZigzagIterator {
    Queue<Iterator<Integer>> its = new LinkedList<Iterator<Integer>>();
    public ZigzagIterator(List<Integer> v1, List<Integer> v2) {
        if (v1.size() > 0) {
            its.add(v1.iterator());
        }
        if (v2.size() > 0) {
            its.add(v2.iterator());
        }
    }

    public int next() {
        Iterator<Integer> it = its.poll();
        int res = it.next();
        if (it.hasNext()) {
            its.add(it);
        }
        return res;
    }

    public boolean hasNext() {
        return its.size() > 0;
    }
}

/**
 * Your ZigzagIterator object will be instantiated and called as such:
 * ZigzagIterator i = new ZigzagIterator(v1, v2);
 * while (i.hasNext()) v[f()] = i.next();
 */
```