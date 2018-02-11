# 149 Max Points on a Line

### Problem
Given n points on a 2D plane, find the maximum number of points that lie on the same straight line.

### Solutions
```java
public class Solution {
    public int maxPoints(Point[] points) {
        int res = 0;
        for (int i = 0; i < points.length; ++i) {
            HashMap<Integer, HashMap<Integer, Integer>> lines = new HashMap<>();
            int duplicate = 1;
            for (int j = i + 1; j < points.length; ++j) {
                if (points[i].x == points[j].x && points[i].y == points[j].y) {
                    duplicate++; 
                    continue;
                }
                int dx = points[j].x - points[i].x;
                int dy = points[j].y - points[i].y;
                int d = gcd(dx, dy);
                if (!lines.containsKey(dx/d)) {
                    lines.put(dx/d, new HashMap<Integer, Integer>());
                }
                if (!lines.get(dx/d).containsKey(dy/d)) {
                    lines.get(dx/d).put(dy/d, 0);
                }
                lines.get(dx/d).put(dy/d, lines.get(dx/d).get(dy/d) + 1);
            }
            res = Math.max(res, duplicate);
            for (Integer a:lines.keySet()) {
                for (Integer b:lines.get(a).keySet()) {
                    res = Math.max(res, lines.get(a).get(b) + duplicate);
                }
            }
        }
        return res;
    }
    // greatest common divisor
    public int gcd(int a, int b) {
        return (b == 0) ? a : gcd(b, a % b);
    }
}
```