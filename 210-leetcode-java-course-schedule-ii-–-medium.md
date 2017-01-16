# 210 LeetCode Java: Course Schedule II – Medium

### Problem:

There are a total of n courses you have to take, labeled from 0 to n - 1.

Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: [0,1]

Given the total number of courses and a list of prerequisite pairs, return the ordering of courses you should take to finish all courses.

There may be multiple correct orders, you just need to return one of them. If it is impossible to finish all courses, return an empty array.

For example:

2, [[1,0]]
There are a total of 2 courses to take. To take course 1 you should have finished course 0. So the correct course order is [0,1]

4, [[1,0],[2,0],[3,1],[3,2]]
There are a total of 4 courses to take. To take course 3 you should have finished both courses 1 and 2. Both courses 1 and 2 should be taken after you finished course 0. So one correct course order is [0,1,2,3]. Another correct ordering is[0,2,1,3].

Note:
The input prerequisites is a graph represented by a list of edges, not adjacency matrices. Read more about how a graph is represented.

### Thoughts:

This is almost identical to the version I of the problem.

Only additional action is that an extra array is needed to store the order of the courses.

Topological sort is by reverse order of finishing time in DFS.

Quotes from my thoughts on version I:

”

This is a very obvious problem on Topological sort. In Introduction to Algorithm, it is the problem of a professor trying to find the order of wearing clothes.

But here, in this problem, it is not asking for the order of courses, but is asking for if it is possible to finish. So it is equivalent to finding if a cycle is in a directed graph.

So a DFS is helpful, because in DFS, whenever you meet GRAY (back edge), it indicates there is a cycle in the directed graph.

The solution below is based on a DFS.

”

### Solutions:

```java
public class Solution {
    int index = 0;
    public int[] findOrder(int numCourses, int[][] prerequisites) {
        HashMap<Integer, List<Integer>> adj = new HashMap<Integer, List<Integer>>();
        int n = numCourses;
        index = n - 1;
        int[][] pre = prerequisites;//make another reference to make variable name shorter
        int[] result = new int[n];
 
        initAdj(n, adj, pre);
 
        int[] color = new int[n];//0 white 1 gray 2 black
        for (int i = 0; i < n; i ++){
            if (!canFinishDFS(adj, color, result, i)){
                return new int[0];
            }
        }//for i
        return result;
    }
    private void initAdj(int n, HashMap<Integer, List<Integer>> adj, int[][] pre){
        for (int i = 0; i < n; i ++){
            adj.put(i, new LinkedList<Integer>());
        }
        for (int i = 0; i < pre.length; i ++){
            adj.get(pre[i][1]).add(pre[i][0]);
        }
    }
    private boolean canFinishDFS(HashMap<Integer, List<Integer>> adj, int[] color, int[] result, int i){
        if (color[i] == 1)
            return false;
        if (color[i] == 2)
            return true;
        color[i] = 1;
        for (Integer j:adj.get(i)){
            if (!canFinishDFS(adj, color, result, j)){
                return false;
            }
        }
        color[i] = 2;
        result[index] = i;
        index --;
        return true;
    }
}
```