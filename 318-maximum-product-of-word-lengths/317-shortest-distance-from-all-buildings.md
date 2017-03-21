# 317. Shortest Distance from All Buildings

You want to build a house on an empty land which reaches all buildings in the shortest amount of distance. You can only move up, down, left and right. You are given a 2D grid of values 0, 1 or 2, where:

Each 0 marks an empty land which you can pass by freely.
Each 1 marks a building which you cannot pass through.
Each 2 marks an obstacle which you cannot pass through.
For example, given three buildings at (0,0), (0,4), (2,2), and an obstacle at (0,2):

```
1 - 0 - 2 - 0 - 1
|   |   |   |   |
0 - 0 - 0 - 0 - 0
|   |   |   |   |
0 - 0 - 1 - 0 - 0
```
The point (1,2) is an ideal empty land to build a house, as the total travel distance of 3+3+1=7 is minimal. So return 7.

### Solutions:

```java
public class Solution {
    public int shortestDistance(int[][] grid) {
        if (grid == null || grid.length == 0 || grid[0].length == 0) {
            return -1;
        }
        Queue<Integer> xs = new LinkedList<Integer>();
        Queue<Integer> ys = new LinkedList<Integer>();
        int[][] sums = new int[grid.length][grid[0].length];
        int[][] reach = new int[grid.length][grid[0].length];
        for (int i = 0; i < grid.length; i ++) {
            for (int j = 0; j < grid[0].length; j ++) {
                if (grid[i][j] == 1) {
                    xs.add(i);
                    ys.add(j);
                }
            }
        }
        int target = xs.size();
        int min = Integer.MAX_VALUE;
        boolean found = false;
        while (!xs.isEmpty()) {
            boolean[][] visited = new boolean[grid.length][grid[0].length];
            int x = xs.poll();
            int y = ys.poll();
            Queue<Integer> qx = new LinkedList<Integer>();
            Queue<Integer> qy = new LinkedList<Integer>();
            Queue<Integer> dis = new LinkedList<Integer>();
            qx.add(x);
            qy.add(y);
            dis.add(0);
            while (!qx.isEmpty()) {
                int i = qx.poll();
                int j = qy.poll();
                int d = dis.poll();
                if (i - 1 >= 0 && visited[i - 1][j] == false && grid[i - 1][j] == 0) {
                    qx.add(i - 1);
                    qy.add(j);
                    dis.add(d + 1);
                    visited[i - 1][j] = true;
                }
                if (i + 1 < grid.length && visited[i + 1][j] == false && grid[i + 1][j] == 0) {
                    qx.add(i + 1);
                    qy.add(j);
                    dis.add(d + 1);
                    visited[i + 1][j] = true;
                }
                if (j - 1 >= 0 && visited[i][j - 1] == false && grid[i][j - 1] == 0) {
                    qx.add(i);
                    qy.add(j - 1);
                    dis.add(d + 1);
                    visited[i][j - 1] = true;
                }
                if (j + 1 < grid[0].length && visited[i][j + 1] == false && grid[i][j + 1] == 0) {
                    qx.add(i);
                    qy.add(j + 1);
                    dis.add(d + 1);
                    visited[i][j + 1] = true;
                }
                if (d != 0) {
                    sums[i][j] += d;
                    reach[i][j] ++;
                    if (xs.isEmpty() && reach[i][j] == target) {
                        found = true;
                        min = Math.min(min, sums[i][j]);
                    }
                }
                
            }
           
           
        }
        if (found == false) {
            return -1;
        }
        return min;
    }
}
```