# 447 Number of Boomerangs

### Problem:
Given n points in the plane that are all pairwise distinct, a "boomerang" is a tuple of points (i, j, k) such that the distance between i and j equals the distance between i and k (the order of the tuple matters).

Find the number of boomerangs. You may assume that n will be at most 500 and coordinates of points are all in the range [-10000, 10000] (inclusive).

Example:
```
Input:
[[0,0],[1,0],[2,0]]

Output:
2

Explanation:
The two boomerangs are [[1,0],[0,0],[2,0]] and [[1,0],[2,0],[0,0]]
```

### Solutions:

```java
public class Solution {
    public int numberOfBoomerangs(int[][] points) {
        int count = 0;
        for (int i = 0; i < points.length; i ++) {
            HashMap<Integer, Integer> sums = new HashMap<Integer, Integer>();
            for (int j = 0; j < points.length; j ++) {
                int d = (points[j][0] - points[i][0]) * (points[j][0] - points[i][0]) + (points[j][1] - points[i][1]) * (points[j][1] - points[i][1]);
                if (!sums.containsKey(d)) {
                    sums.put(d, 1);
                }
                else {
                    sums.put(d, sums.get(d) + 1);
                }
            }
            for (Integer sum:sums.keySet()) {
                count += sums.get(sum) * (sums.get(sum) - 1);
            }
        }
        return count;
    }
}
```