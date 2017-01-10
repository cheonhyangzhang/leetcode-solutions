# 251 LeetCode Java: Count Univalue Subtrees – Medium

#Problem:

Implement an iterator to flatten a 2d vector.

For example,
Given 2d vector =

[
  [1,2],
  [3],
  [4,5,6]
]
By calling next repeatedly until hasNext returns false, the order of elements returned by next should be: [1,2,3,4,5,6].

Hint:

How many variables do you need to keep track?
 

# Thoughts:

A straightforward way is to flatten the 2D array into a 1D array in the constructor, then everything is easy. But this is not efficient.

When can use two Integer to represent the current index in the 2D array, and it starts with 0 and 0. We need to update the index when we call next() and hasNext().

Actually by using two Iterator is making the problem much easier.
It’s similar to two Integer index, we might need to update the two Iterator when we call next() and hasNext().
E.g [[1],[],[2,3]].

# Solutions:

```java
public class Vector2D implements Iterator<Integer> {
    Iterator<List<Integer>> vi;
    Iterator<Integer> hi;
    public Vector2D(List<List<Integer>> vec2d) {
        vi = vec2d.iterator();
    }
    private void check() {
        if (hi == null || !hi.hasNext()) {
            while (vi.hasNext()) {
            hi = vi.next().iterator();
                if (hi.hasNext()) {
                    return;
                }
            }
        }
    }
    @Override
    public Integer next() {
        check();
        return hi.next();
    }
 
    @Override
    public boolean hasNext() {
        check();
        if (hi == null) {
            return false;
        }
        return hi.hasNext();
    }
}
 
/**
 * Your Vector2D object will be instantiated and called as such:
 * Vector2D i = new Vector2D(vec2d);
 * while (i.hasNext()) v[f()] = i.next();
 */
 ```