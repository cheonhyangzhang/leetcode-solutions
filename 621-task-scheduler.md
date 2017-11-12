# 621 Task Scheduler

### Problem
Given a char array representing tasks CPU need to do. It contains capital letters A to Z where different letters represent different tasks.Tasks could be done without original order. Each task could be done in one interval. For each interval, CPU could finish one task or just be idle.

However, there is a non-negative cooling interval n that means between two same tasks, there must be at least n intervals that CPU are doing different tasks or just be idle.

You need to return the least number of intervals the CPU will take to finish all the given tasks.

Example 1:
Input: tasks = ["A","A","A","B","B","B"], n = 2
Output: 8
Explanation: A -> B -> idle -> A -> B -> idle -> A -> B.
Note:
The number of tasks is in the range [1, 10000].
The integer n is in the range [0, 100].

### Solutions

```java
class Solution {
    class Node implements Comparable<Node>{
        public char c;
        public int count;
        public Node (char c, int count) {
            this.c = c;
            this.count = count;
        }
        public int compareTo(Node n) {
            return n.count - this.count;
        }
    }
    public int leastInterval(char[] tasks, int n) {
        PriorityQueue<Node> q = new PriorityQueue<Node>();
        HashMap<Character, Integer> count = new HashMap<Character, Integer>();
        for (int i = 0; i < tasks.length; i ++) {
            char task = tasks[i];
            if (!count.containsKey(task)) {
                count.put(task, 0);
            }
            count.put(task, count.get(task) + 1);
        }
        for (Character c:count.keySet()) {
            q.add(new Node(c, count.get(c)));
        }
        int res = 0;
        while (!q.isEmpty()) {
            List<Node> add = new LinkedList<Node>();
            for (int i = 0; i < n + 1; i ++) {
                if (q.isEmpty() && add.isEmpty()) {
                    break;
                }
                if (!q.isEmpty()) {
                    Node node = q.poll();
                    node.count --;
                    if (node.count != 0) {
                        add.add(node);
                    }
                }
                res ++;
            }
            for (Node node:add) {
                q.add(node);
            }
        }
        return res;
    }
}
```