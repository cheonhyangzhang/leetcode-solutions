# 261. Graph Valid Tree - Medium

# Problem:

Given n nodes labeled from 0 to n - 1 and a list of undirected edges (each edge is a pair of nodes), write a function to check whether these edges make up a valid tree.

For example:

Given n = 5 and edges = [[0, 1], [0, 2], [0, 3], [1, 4]], return true.

Given n = 5 and edges = [[0, 1], [1, 2], [2, 3], [1, 3], [1, 4]], return false.

Show Hint 
Note: you can assume that no duplicate edges will appear in edges. Since all edges are undirected, [0, 1] is the same as [1, 0] and thus will not appear together in edges.

# Solutions:

DFS
```java
public class Solution {
    public boolean validTree(int n, int[][] edges) {
        HashMap<Integer, List<Integer>> adj = new HashMap<Integer, List<Integer>>();
        init(adj, edges);
        int[] color = new int[n]; // 0 is white 1 is gray and 2 is black
        if (!dfsVisit(-1, 0, adj, color)) {
            return false;
        }
        for (int i = 0; i < color.length; i ++) {
            if (color[i] == 0) {
                return false;
            }
        }
        return true;
    }
    private void init(HashMap<Integer, List<Integer>> adj, int[][] edges) {
        for (int i = 0; i < edges.length; i ++) {
            if (!adj.containsKey(edges[i][0])) {
                adj.put(edges[i][0], new LinkedList<Integer>());
            }
            adj.get(edges[i][0]).add(edges[i][1]);
            if (!adj.containsKey(edges[i][1])) {
                adj.put(edges[i][1], new LinkedList<Integer>());
            }
            adj.get(edges[i][1]).add(edges[i][0]);
        }
    }
    private boolean dfsVisit(int parent, int index, HashMap<Integer, List<Integer>> adj, int[] color) {
        if (color[index] != 0) {
            return false;
        }
        color[index] = 1;
        if (adj.containsKey(index)) {
            for (Integer i:adj.get(index)) {
                if (parent != i && !dfsVisit(index, i, adj, color)) {
                    return false;
                }
            }
        }
        return true;
    }
}
```

BFS

```java
public class Solution {
    public boolean validTree(int n, int[][] edges) {
        HashMap<Integer, List<Integer>> adj = new HashMap<Integer, List<Integer>>();
        init(adj, edges);
        int[] color = new int[n]; // 0 is white 1 is gray and 2 is black
        Queue<Integer> q = new LinkedList<Integer>();
        q.add(0);
        while (q.size() > 0) {
            int index = q.poll();
            if (color[index] != 0) {
                return false;
            }
            if (adj.containsKey(index)) {
                for (Integer i:adj.get(index)) {
                    if (color[i] == 0) {
                        q.add(i);
                    }
                }
            }
            color[index] = 1;
        }
        for (int i = 0; i < color.length; i ++) {
            if (color[i] == 0) {
                return false;
            }
        }
        return true;
    }
    private void init(HashMap<Integer, List<Integer>> adj, int[][] edges) {
        for (int i = 0; i < edges.length; i ++) {
            if (!adj.containsKey(edges[i][0])) {
                adj.put(edges[i][0], new LinkedList<Integer>());
            }
            adj.get(edges[i][0]).add(edges[i][1]);
            if (!adj.containsKey(edges[i][1])) {
                adj.put(edges[i][1], new LinkedList<Integer>());
            }
            adj.get(edges[i][1]).add(edges[i][0]);
        }
    }
}
```