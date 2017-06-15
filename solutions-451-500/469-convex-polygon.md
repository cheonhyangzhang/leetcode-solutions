# 469 Convex Polygon

### Problem:

Given a list of points that form a polygon when joined sequentially, find if this polygon is convex (Convex polygon definition).

Note:

There are at least 3 and at most 10,000 points.
Coordinates are in the range -10,000 to 10,000.
You may assume the polygon formed by given points is always a simple polygon (Simple polygon definition). In other words, we ensure that exactly two edges intersect at each vertex, and that edges otherwise don't intersect each other.

Example 1:
```
[[0,0],[0,1],[1,1],[1,0]]

Answer: True

Explanation:
```
![](/assets/1.png)

Example 2:
```
[[0,0],[0,10],[10,10],[10,0],[5,5]]

Answer: False

Explanation:
```
![](/assets/2.png)

### Solutions:

```java
public class Solution {
    public boolean isConvex(List<List<Integer>> points) {
        int n = points.size();
        int pre = 0, cur = 0;
        for (int i = 0; i < n; ++i) {
            int dx1 = points.get((i + 1) % n).get(0) - points.get(i).get(0);
            int dx2 = points.get((i + 2) % n).get(0) - points.get(i).get(0);
            int dy1 = points.get((i + 1) % n).get(1) - points.get(i).get(1);
            int dy2 = points.get((i + 2) % n).get(1) - points.get(i).get(1);
            cur = dx1 * dy2 - dx2 * dy1;
            if (cur != 0) {
                if ((cur > 0 && pre < 0) || (cur < 0 && pre > 0)) 
                    return false;
                else 
                    pre = cur;
            }
        }
        return true;
    }
}
```