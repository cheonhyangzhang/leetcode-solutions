# 305 Number of Islands II

A 2d grid map of m rows and n columns is initially filled with water. We may perform an addLand operation which turns the water at position (row, col) into a land. Given a list of positions to operate, count the number of islands after each addLand operation. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

Example:

Given m = 3, n = 3, positions = [[0,0], [0,1], [1,2], [2,1]].
Initially, the 2d grid grid is filled with water. (Assume 0 represents water and 1 represents land).

```
0 0 0
0 0 0
0 0 0
```

Operation #1: addLand(0, 0) turns the water at grid[0][0] into a land.

```
1 0 0
0 0 0   Number of islands = 1
0 0 0
```
Operation #2: addLand(0, 1) turns the water at grid[0][1] into a land.
```
1 1 0
0 0 0   Number of islands = 1
0 0 0
```
Operation #3: addLand(1, 2) turns the water at grid[1][2] into a land.
```
1 1 0
0 0 1   Number of islands = 2
0 0 0
```
Operation #4: addLand(2, 1) turns the water at grid[2][1] into a land.
```
1 1 0
0 0 1   Number of islands = 3
0 1 0
```
We return the result as an array: [1, 1, 2, 3]

Challenge:

Can you do it in time complexity O(k log mn), where k is the length of the positions?

### Solutions:

```java
public class Solution {
    private class Node {
        public Node parent;
        public int rank;
        public Node() {
            parent = null;
            rank = -1;
        }
    }
    HashMap<String,Node> nodes;
    public List<Integer> numIslands2(int m, int n, int[][] positions) {
        List<Integer> result = new LinkedList<Integer>();
        nodes = new HashMap<String, Node>();
        int num = 0;
        for (int i = 0; i < positions.length; i ++) {
            int x = positions[i][0];
            int y = positions[i][1];
            Node added = makeset(x, y);
            num ++;
            if (x - 1 >= 0 && nodes.containsKey((x-1) + "," + y)) {
                Node node = nodes.get((x-1) + "," + y);
                boolean tmp = union(added, node);
                if (tmp) {
                    num --; 
                }
            }
            if (x + 1 < m && nodes.containsKey((x+1) + "," + y)) {
                Node node = nodes.get((x+1) + "," + y);
                boolean tmp = union(added, node);
                if (tmp) {
                    num --; 
                }
            }
            if (y - 1 >= 0 && nodes.containsKey(x + "," + (y - 1))) {
                Node node = nodes.get(x + "," + (y - 1));
                boolean tmp = union(added, node);
                if (tmp) {
                    num --; 
                }
            }
            if (y + 1 < n && nodes.containsKey(x + "," + (y + 1))) {
                Node node = nodes.get(x + "," + (y + 1));
                boolean tmp = union(added, node);
                if (tmp) {
                    num --; 
                }
            }
            result.add(num);
        }
        return result;
    }
    private boolean union(Node n1, Node n2) {
        Node root1 = find(n1);
        Node root2 = find(n2);
        if (root1 == root2) {
            return false;
        }
        if (root1.rank < root2.rank) {
            root1.parent = root2;
        }
        else if (root1.rank > root2.rank) {
            root2.parent = root1;
        }
        else {
            root2.parent = root1;
            root1.rank += 1;
        }
        return true;
    }
    private Node find(Node n) {
        if (n.parent == n) {
            return n;
        }
        else {
            return find(n.parent);
        }
    }
    private Node makeset(int x, int y) {
        Node n = new Node();
        n.parent = n;
        n.rank = 0;
        nodes.put(x +","+ y, n);
        return n;
    }
    
}
```