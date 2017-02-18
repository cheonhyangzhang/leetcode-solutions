# 490 The Maze

### Problem:
There is a ball in a maze with empty spaces and walls. The ball can go through empty spaces by rolling up, down, left or right, but it won't stop rolling until hitting a wall. When the ball stops, it could choose the next direction.

Given the ball's start position, the destination and the maze, determine whether the ball could stop at the destination.

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

Output: true
Explanation: One possible way is : left -> down -> left -> down -> right -> down -> right.
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

Output: false
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
    public boolean hasPath(int[][] maze, int[] start, int[] destination) {
        int[][] visited = new int[maze.length][maze[0].length];
        //0000 means not direction is visted.
        //NESW so that 0010 means South is visited. 
        return reach(maze, start[0], start[1] , destination, visited);
    }
    private boolean reach(int[][] maze, int i, int j, int[] dest, int[][] visited) {
        System.out.println("visit : " + i + ", " + j);
        if (i == dest[0] && j == dest[1]) {
            return true;
        }
        if (visited[i][j] == 15) {
            return false;
        }
        if (canGo(maze, i - 1, j) && !hasVisited(visited, i, j, 8)) {
            visited[i][j] |= 8;
            int m = i;
            while (m >= 0 && maze[m][j] == 0) {
                m --;
            }
            m ++;
            visited[m][j] |= 2;
            if (reach(maze, m, j, dest, visited)) {
                return true;
            }
        }
        if (canGo(maze, i, j + 1) && !hasVisited(visited, i, j, 4)) {
            visited[i][j] |= 4;
            int n = j;
            while ( n < maze[0].length && maze[i][n] == 0) {
                n ++;
            }
            n --;
            visited[i][n] |= 1;
            if (reach(maze, i, n, dest, visited)) {
                return true;
            }
        }
        if (canGo(maze, i + 1, j) && !hasVisited(visited, i, j, 2)) {
            visited[i][j] |= 2;
            int m = i;
            while (m < maze.length && maze[m][j] == 0) {
                m ++;
            }
            m --;
            visited[m][j] |= 8;
            if (reach(maze, m, j, dest, visited)) {
                return true;
            }
        }
        if (canGo(maze, i, j - 1) && !hasVisited(visited, i, j, 1)) {
            visited[i][j] |= 1;
            int n = j;
            while (n >= 0 && maze[i][n] == 0) {
                n --;
            }
            n ++;
            visited[i][n] |= 4;
            if (reach(maze, i, n, dest, visited)) {
                return true;
            }
        }
        return false;
    }
    private boolean hasVisited(int[][] visited, int i, int j, int dir) {
        return (visited[i][j]&dir) == dir;
    }
    private boolean canGo(int[][] maze, int i, int j) {
        if (i >= 0 && i < maze.length && j >= 0 && j < maze[0].length && maze[i][j] == 0) {
            return true;
        }
        return false;
    }
}
```