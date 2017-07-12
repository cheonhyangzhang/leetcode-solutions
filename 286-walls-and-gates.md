# 286 Walls and Gates

### Problem:

<pre>
You are given a m x n 2D grid initialized with these three possible values.

-1 - A wall or an obstacle.
0 - A gate.
INF - Infinity means an empty room. We use the value 2^31 - 1 = 2147483647 to represent INF as you may assume that the distance to a gate is less than 2147483647.
Fill each empty room with the distance to its nearest gate. If it is impossible to reach a gate, it should be filled with INF.

For example, given the 2D grid:
INF  -1  0  INF
INF INF INF  -1
INF  -1 INF  -1
  0  -1 INF INF
After running your function, the 2D grid should be:
  3  -1   0   1
  2   2   1  -1
  1  -1   2  -1
  0  -1   3   4
</pre>

### Solution:

```java
public class Solution {
    public void wallsAndGates(int[][] rooms) {
        for (int i = 0; i < rooms.length; i ++) {
            for (int j = 0; j < rooms[0].length; j ++) {
                if (rooms[i][j] == 0) {
                    visit(rooms, i, j, 0);
                }
            }
        }
    }
    private void visit(int[][] rooms, int i, int j, int step) {
        if (i < 0 || j < 0 || i >= rooms.length || j >= rooms[0].length || rooms[i][j] < step) {
            return;
        }
        rooms[i][j] = step;
        visit(rooms, i - 1, j, step + 1);
        visit(rooms, i, j - 1, step + 1);
        visit(rooms, i + 1, j, step + 1);
        visit(rooms, i, j + 1, step + 1);
    }
}
```

```java
public class Solution {
    public void wallsAndGates(int[][] rooms) {
        if (rooms == null || rooms.length == 0 || rooms[0].length == 0) {
            return;
        }
        Queue<Integer> q = new LinkedList<Integer>();
        int m = rooms.length;
        int n = rooms[0].length;
        for (int i = 0; i < m; i ++) {
            for (int j = 0; j < n; j ++) {
                if (rooms[i][j] == 0) {
                    q.add(i * n + j);
                }
            }
        }
        while (q.size() > 0) {
            int tmp = q.poll();
            int x = tmp / n;
            int y = tmp % n;
            if (x > 0 && rooms[x-1][y] ==Integer.MAX_VALUE) {
                rooms[x-1][y] = rooms[x][y] + 1;
                q.add((x-1) * n + y);
            }
            if (x < m - 1 && rooms[x+1][y] ==Integer.MAX_VALUE) {
                rooms[x+1][y] = rooms[x][y] + 1;
                q.add((x+1) * n + y);
            }
            if (y > 0 && rooms[x][y-1] ==Integer.MAX_VALUE) {
                rooms[x][y-1] = rooms[x][y] + 1;
                q.add(x * n + y - 1);
            }
            if (y < n - 1 && rooms[x][y+1] ==Integer.MAX_VALUE) {
                rooms[x][y+1] = rooms[x][y] + 1;
                q.add(x * n + y + 1);
            }
        }
    }
}
```