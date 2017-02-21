# 505. The Maze II

### Problem:

There is a ball in a maze with empty spaces and walls. The ball can go through empty spaces by rolling up, down, left or right, but it won't stop rolling until hitting a wall. When the ball stops, it could choose the next direction.

Given the ball's start position, the destination and the maze, find the shortest distance for the ball to stop at the destination. The distance is defined by the number of empty spaces traveled by the ball from the start position (excluded) to the destination (included). If the ball cannot stop at the destination, return -1.

The maze is represented by a binary 2D array. 1 means the wall and 0 means the empty space. You may assume that the borders of the maze are all walls. The start and destination coordinates are represented by row and column indexes.

Example 1
```
Input 1: a maze represented by a 2D array

0 0 1 0 0
0 0 0 0 0
0 0 0 1 0
1 1 0 1 1
0 0 0 0 0

Input 2: start coordinate (rowStart, colStart) = (0, 4)
Input 3: destination coordinate (rowDest, colDest) = (4, 4)

Output: 12
Explanation: One shortest way is : left -> down -> left -> down -> right -> down -> right.
             The total distance is 1 + 1 + 3 + 1 + 2 + 2 + 2 = 12.
```
![](/assets/maze_1_example_1.png)

Example 2
```
Input 1: a maze represented by a 2D array

0 0 1 0 0
0 0 0 0 0
0 0 0 1 0
1 1 0 1 1
0 0 0 0 0

Input 2: start coordinate (rowStart, colStart) = (0, 4)
Input 3: destination coordinate (rowDest, colDest) = (3, 2)

Output: -1
Explanation: There is no way for the ball to stop at the destination.
```
![](/assets/maze_1_example_2.png)

Note:
1. There is only one ball and one destination in the maze.
2. Both the ball and the destination exist on an empty space, and they will not be at the same position initially.
3. The given maze does not contain border (like the red rectangle in the example pictures), but you could assume the border of the maze are all walls.
4. The maze contains at least 2 empty spaces, and both the width and height of the maze won't exceed 100.

### Solutions:

```java
public class Solution {
    private class Point implements Comparable<Point>{
        public int x;
        public int y;
        public int step;
        public Point(int x, int y, int step) {
            this.x = x;
            this.y = y;
            this.step = step;
        }
        public int compareTo(Point p) {
            return this.step - p.step;
        }
    }
    public int shortestDistance(int[][] maze, int[] start, int[] destination) {
        int[][] dirs = new int[4][2];
        dirs[0] = new int[]{1, 0};
        dirs[1] = new int[]{0, 1};
        dirs[2] = new int[]{-1, 0};
        dirs[3] = new int[]{0, -1};
        boolean[][] visited = new boolean[maze.length][maze[0].length];
        PriorityQueue<Point> q = new PriorityQueue<Point>();
        q.add(new Point(start[0], start[1], 0));
        while (!q.isEmpty()) {
            Point p = q.poll();
            if (p.x == destination[0] && p.y == destination[1]) {
                return p.step;
            }
            visited[p.x][p.y] = true;
            for (int k = 0; k < dirs.length; k ++) {
                int i = p.x;
                int j = p.y;
                int count = 0;
                while (i >= 0 && i < maze.length && j >= 0 && j < maze[0].length && maze[i][j] == 0) {
                    i += dirs[k][0];
                    j += dirs[k][1];
                    count ++;
                }
                i -= dirs[k][0];
                j -= dirs[k][1];
                count --;
                if (visited[i][j] == false) {
                    q.add(new Point(i, j, p.step + count));
                }
            }
        }
        return -1;
    }
        
      
}
```