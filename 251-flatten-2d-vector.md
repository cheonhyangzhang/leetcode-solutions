# 251 Flatten 2D Vector

#Problem:

Implement an iterator to flatten a 2d vector.

For example,
Given 2d vector =
```
[
  [1,2],
  [3],
  [4,5,6]
]
```
By calling next repeatedly until hasNext returns false, the order of elements returned by next should be: [1,2,3,4,5,6].

Follow up:
As an added challenge, try to code it using only iterators in C++ or iterators in Java. 

# Thoughts:

A straightforward way is to flatten the 2D array into a 1D array in the constructor, then everything is easy. But this is not efficient.

When can use two Integer to represent the current index in the 2D array, and it starts with 0 and 0. We need to update the index when we call next() and hasNext().

Actually by using two Iterator is making the problem much easier.
It’s similar to two Integer index, we might need to update the two Iterator when we call next() and hasNext().
E.g [[1],[],[2,3]].

# Solutions:
 
 ```java
 public class Vector2D implements Iterator<Integer> {
    Integer next = null;
    Iterator<List<Integer>> vi = null;
    Iterator<Integer> hi = null;
    public Vector2D(List<List<Integer>> vec2d) {
        vi = vec2d.iterator();
        if (vi.hasNext()) {
            hi = vi.next().iterator();
        }
        findNext();
    }
    private void findNext() {
        if (hi == null) {
            return;
        }
        next = null;
        if (hi.hasNext()) {
            next = hi.next();
            return;
        }
        while (vi.hasNext()) {
            hi = vi.next().iterator();
            if (hi.hasNext()) {
                next = hi.next();
                break;
            }
        }
    }

    @Override
    public Integer next() {
        Integer res = next;
        findNext();
        return res;
    }

    @Override
    public boolean hasNext() {
        return next != null;
    }
}

/**
 * Your Vector2D object will be instantiated and called as such:
 * Vector2D i = new Vector2D(vec2d);
 * while (i.hasNext()) v[f()] = i.next();
 */
 ```