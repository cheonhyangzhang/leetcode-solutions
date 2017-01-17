# 323. Number of Connected Components in an Undirected Graph

### Problem:

<pre>
Given n nodes labeled from 0 to n - 1 and a list of undirected edges (each edge is a pair of nodes), write a function to find the number of connected components in an undirected graph.

Example 1:
     0          3
     |          |
     1 --- 2    4
Given n = 5 and edges = [[0, 1], [1, 2], [3, 4]], return 2.

Example 2:
     0           4
     |           |
     1 --- 2 --- 3
Given n = 5 and edges = [[0, 1], [1, 2], [2, 3], [3, 4]], return 1.

Note:
You can assume that no duplicate edges will appear in edges. Since all edges are undirected, [0, 1] is the same as [1, 0] and thus will not appear together in edges.
</pre>

### Solutions:

```java
public class Solution {
    public int countComponents(int n, int[][] edges) {
        HashMap<Integer, List<Integer>> adj = new HashMap<Integer, List<Integer>>();
        init(adj, edges, n);
        boolean[] visited = new boolean[n];
        int count = 0;
        for (int i = 0; i < n; i ++) {
            if (visited[i] == false) {
                count ++;
                dfs(adj, i, visited);
            }
        }
        return count;
    }
    private void dfs(HashMap<Integer, List<Integer>> adj, int index, boolean[] visited) {
        visited[index] = true;
        for (Integer j:adj.get(index)) {
            if (visited[j] == false) {
                dfs(adj, j, visited);
            }
        }
    }
    private void init(HashMap<Integer, List<Integer>> adj, int[][] edges, int n) {
        for (int i = 0; i < n; i ++) {
            adj.put(i, new LinkedList<Integer>());
        }
        for (int i = 0; i < edges.length; i ++) {
            adj.get(edges[i][0]).add(edges[i][1]);
            adj.get(edges[i][1]).add(edges[i][0]);
        }
    }
}
```

```java
public class Solution {
    public int countComponents(int n, int[][] edges) {
        int[] root = new int[n];
        for (int i = 0; i < n; i ++) {
            root[i] = i;
        }
        int count = n;
        for (int i = 0; i < edges.length; i ++) {
            int r1 = getRoot(root, edges[i][0]);
            int r2 = getRoot(root, edges[i][1]);
            if (r1 != r2) {
                root[r1] = r2;
                count --;
            }
        }
        return count;
    }
    private int getRoot(int[] root, int i) {
        while (root[i] != i) {
            root[i] = root[root[i]];
            i = root[i];
        }
        return i;
    }
}
```