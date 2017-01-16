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
    private int next = 0;
    public int[] findOrder(int numCourses, int[][] prerequisites) {
        HashMap<Integer, LinkedList<Integer>> adj = new HashMap<Integer, LinkedList<Integer>>();
        next = numCourses - 1;
        initAdj(adj, prerequisites);
        int[] result = new int[numCourses];
        int[] color = new int[numCourses]; // 0 is white, 1 is gray, 2 is black
        for (int i = 0; i < color.length; i ++) {
            if (color[i] == 0) {
                if (!dfsVisit(adj, i,color, result)) {
                    return new int[0];
                }
            }
        }
        return result;
    }
    private boolean dfsVisit(HashMap<Integer, LinkedList<Integer>> adj, int index, int[] color, int[] result) {
        color[index] = 1;
        if (adj.containsKey(index)) {
            for (Integer j:adj.get(index)) {
                if (color[j] == 1) {
                    return false;
                }
                if (color[j] == 0) {
                    if (!dfsVisit(adj, j, color, result)) {
                        return false;
                    }
                }
                 
            }
        }
        result[next] = index;
        next --;
        color[index] = 2;
        return true;
    }
    private void initAdj(HashMap<Integer, LinkedList<Integer>> adj, int[][] pre) {
        for (int i = 0; i < pre.length; i ++) {
            if (!adj.containsKey(pre[i][1])) {
                adj.put(pre[i][1], new LinkedList<Integer>());
            }
            adj.get(pre[i][1]).add(pre[i][0]);
        }
    }
}
```