
# 356 Line Reflection

### Problem:

Given n points on a 2D plane, find if there is such a line parallel to y-axis that reflect the given points.

Example 1:
Given points = [[1,1],[-1,1]], return true.

Example 2:
Given points = [[1,1],[-1,-1]], return false.

Follow up:
Could you do better than O(n2)?

Hint:

Find the smallest and largest x-value for all points.
If there is a line then it should be at y = (minX + maxX) / 2.
For each point, make sure that it has a reflected point in the opposite side.

### Solutions:

```java
public class Solution {
    public boolean isReflected(int[][] points) {
        int min = Integer.MAX_VALUE;
        int max = Integer.MIN_VALUE;
        HashMap<Integer, HashSet<Integer>> ys = new HashMap<Integer, HashSet<Integer>>();
        for (int i = 0; i < points.length; i ++) {
            int x = points[i][0];
            int y = points[i][1];
            min = Math.min(min, x);
            max = Math.max(max, x);
            if (!ys.containsKey(x)) {
                ys.put(x, new HashSet<Integer>());
            }
            ys.get(x).add(y);
        }
        int doublebar = (min + max);
        for (int i = 0; i < points.length; i ++) {
            int x = points[i][0];
            int y = points[i][1];
            int mx = doublebar - x;
            if (!ys.containsKey(mx)) {
                return false;
            }
            if (!ys.get(mx).contains(y)) {
                return false;
            }
        }
        
        return true;
    }
}
```

```java
class Solution {
    public boolean isReflected(int[][] points) {
        int min = Integer.MAX_VALUE;
        int max = Integer.MIN_VALUE;
        HashMap<Integer, HashSet<Integer>> ys = new HashMap<Integer, HashSet<Integer>>();
        for (int i = 0; i < points.length; i ++) {
            int x = points[i][0];
            int y = points[i][1];
            min = Math.min(min, x);
            max = Math.max(max, x);
            if (!ys.containsKey(y)) {
                ys.put(y, new HashSet<Integer>());
            }
            ys.get(y).add(x);
        }
        int doublebar = (min + max);
        for (Integer y:ys.keySet()) {
            for (Integer x:ys.get(y)) {
                int mx = doublebar - x;
                if (!ys.get(y).contains(mx)) {
                    return false;
                }
            }
        }
        return true;
    }
}
```