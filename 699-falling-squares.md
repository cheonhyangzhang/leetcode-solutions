# 699 Falling Squares

### Problem
On an infinite number line (x-axis), we drop given squares in the order they are given.

The i-th square dropped (positions[i] = (left, side_length)) is a square with the left-most point being positions[i][0] and sidelength positions[i][1].

The square is dropped with the bottom edge parallel to the number line, and from a higher height than all currently landed squares. We wait for each square to stick before dropping the next.

The squares are infinitely sticky on their bottom edge, and will remain fixed to any positive length surface they touch (either the number line or another square). Squares dropped adjacent to each other will not stick together prematurely.


Return a list ans of heights. Each height ans[i] represents the current highest height of any square we have dropped, after dropping squares represented by positions[0], positions[1], ..., positions[i].

Example 1:
```
Input: [[1, 2], [2, 3], [6, 1]]
Output: [2, 5, 5]
Explanation:

After the first drop of positions[0] = [1, 2]:
_aa
_aa
-------
The maximum height of any square is 2.


After the second drop of positions[1] = [2, 3]:
__aaa
__aaa
__aaa
_aa__
_aa__
--------------
The maximum height of any square is 5.  
The larger square stays on top of the smaller square despite where its center
of gravity is, because squares are infinitely sticky on their bottom edge.


After the third drop of positions[1] = [6, 1]:
__aaa
__aaa
__aaa
_aa
_aa___a
--------------
The maximum height of any square is still 5.

Thus, we return an answer of [2, 5, 5].
```
Example 2:
```
Input: [[100, 100], [200, 100]]
Output: [100, 100]
Explanation: Adjacent squares don't get stuck prematurely - only their bottom edge can stick to surfaces.
```

Note:

1 <= positions.length <= 1000.
1 <= positions[i][0] <= 10^8.
1 <= positions[i][1] <= 10^6.


```java
class Solution {
    public List<Integer> fallingSquares(int[][] positions) {
        List<Integer> res = new LinkedList<>();
        TreeMap<Integer, int[]> ranges = new TreeMap<>();
        int max = 0;
        ranges.put(0, new int[]{0, 0});
        for (int i = 0; i < positions.length; i ++) {
            int start = positions[i][0];
            int len = positions[i][1];
            int end = positions[i][0] + len;
            int belowHeight = 0;
            Integer key = ranges.lowerKey(start + 1);
            HashMap<Integer, int[]> add = new HashMap<>();
            while (key != null && (key == 0 || key < end)) {
                if (key == 0) {
                    key = ranges.higherKey(key);
                    continue;
                }
                int itstart = key;
                int itend = ranges.get(key)[0];
                int itheight = ranges.get(key)[1];
                if (itend <= start || itstart >= end) {
                    key = ranges.higherKey(key);
                    continue;
                }
                if (itstart < start && itend > start) {
                    add.put(itstart, new int[]{start, itheight});
                }
                if (itstart < end && itend > end) {
                    add.put(end, new int[]{ itend, itheight});
                }
                
                ranges.remove(key);
                belowHeight = Math.max(belowHeight, itheight);
                key = ranges.higherKey(key);
            }
            ranges.put(start, new int[]{end, belowHeight + len});
            for (Integer addkey:add.keySet()) {
                ranges.put(addkey, add.get(addkey));
            }
            max = Math.max(max, belowHeight + len);
            res.add(max);
        }
        
        return res;
    }
}
```