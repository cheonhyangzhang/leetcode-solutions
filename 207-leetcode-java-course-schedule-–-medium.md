# 207 LeetCode Java: Course Schedule – Medium

### Problem:

There are a total of n courses you have to take, labeled from 0 to n - 1.

Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: [0,1]

Given the total number of courses and a list of prerequisite pairs, is it possible for you to finish all courses?

For example:

2, [[1,0]]
There are a total of 2 courses to take. To take course 1 you should have finished course 0. So it is possible.

2, [[1,0],[0,1]]
There are a total of 2 courses to take. To take course 1 you should have finished course 0, and to take course 0 you should also have finished course 1. So it is impossible.

Note:
The input prerequisites is a graph represented by a list of edges, not adjacency matrices. Read more about how a graph is represented.

Hints:

This problem is equivalent to finding if a cycle exists in a directed graph. If a cycle exists, no topological ordering exists and therefore it will be impossible to take all courses.
### Thoughts:

This is a very obvious problem on Topological sort. In Introduction to Algorithm, it is the problem of a professor trying to find the order of wearing clothes.

But here, in this problem, it is not asking for the order of courses, but is asking for if it is possible to finish. So it is equivalent to finding if a cycle is in a directed graph.

So a DFS is helpful, because in DFS, whenever you meet GRAY (back edge), it indicates there is a cycle in the directed graph.

The solution below is based on a DFS.

### Solutions:
```java
public class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        HashMap<Integer, List<Integer>> adj = new HashMap<Integer, List<Integer>>();
        int[] color = new int[numCourses];//0 is white, 1 is gray 2, is black
        initAdj(adj, prerequisites);
        for (int i = 0; i < numCourses; i ++) {
            if (color[i] == 1) {
                return false;
            }
            if (color[i] == 0) {
                //DFS visit
                if (dfsVisit(adj, color, i) == false) {
                    return false;
                }
            }
        }
        return true;
    }
    private boolean dfsVisit(HashMap<Integer, List<Integer>> adj, int[] color, int i) {
        if (!adj.containsKey(i)) {
            color[i] = 2;
            return true;
        }
        color[i] = 1;
        for (Integer j:adj.get(i)) {
            if (color[j] == 1) {
                return false;
            }
            if (color[j] == 0) {
                if (dfsVisit(adj, color, j) == false) {
                    return false;
                }
            }
        }
        color[i] = 2;
        return true;
    }
    private void initAdj(HashMap<Integer, List<Integer>> adj , int[][] pre) {
        for (int i = 0; i < pre.length; i ++) {
            if (!adj.containsKey(pre[i][1])) {
                adj.put(pre[i][1], new LinkedList());
            }
            adj.get(pre[i][1]).add(pre[i][0]);
        }
    }
}```