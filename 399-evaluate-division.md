# 399 Evaluate Division

### Problem:

Total Accepted: 10747
Total Submissions: 26763
Difficulty: Medium
Contributors: Admin
Equations are given in the format A / B = k, where A and B are variables represented as strings, and k is a real number (floating point number). Given some queries, return the answers. If the answer does not exist, return -1.0.

Example:
Given a / b = 2.0, b / c = 3.0. 
queries are: a / c = ?, b / a = ?, a / e = ?, a / a = ?, x / x = ? . 
return [6.0, 0.5, -1.0, 1.0, -1.0 ].

The input is: vector<pair<string, string>> equations, vector<double>& values, vector<pair<string, string>> queries , where equations.size() == values.size(), and the values are positive. This represents the equations. Return vector<double>.

According to the example above:
```
equations = [ ["a", "b"], ["b", "c"] ],
values = [2.0, 3.0],
queries = [ ["a", "c"], ["b", "a"], ["a", "e"], ["a", "a"], ["x", "x"] ]. 
```

The input is always valid. You may assume that evaluating the queries will result in no division by zero and there is no contradiction.

### Solutions:

```java
public class Solution {
    public double[] calcEquation(String[][] equations, double[] values, String[][] queries) {
        HashMap<String, List<String>> adj = new HashMap<String, List<String>>();
        HashMap<String, Double> vals = new HashMap<String, Double>();
        init(equations, values, adj, vals);
        
        double[] result = new double[queries.length];
        for (int i = 0; i < queries.length; i ++) {
            result[i] = process(queries[i][0], queries[i][1], adj, vals);
        }
        return result;
    }
    private double process(String up, String down, HashMap<String, List<String>> adj, HashMap<String, Double> vals) {
        if (!adj.containsKey(up) || !adj.containsKey(down)) {
            return -1.0;
        }
        HashSet<String> visited = new HashSet<String>();
        Queue<String> q = new LinkedList<String>();
        Queue<Double> data = new LinkedList<Double>();
        q.add(up);
        data.add(1.0);
        double result = 1;
        while (!q.isEmpty()) {
            String s = q.poll();
            Double v = data.poll();
            if (visited.contains(s)) {
                continue;
            }
            visited.add(s);
            if (s.equals(down)) {
                return v;
            }
            for (String str:adj.get(s)) {
                if (visited.contains(str)) {
                    continue;
                }
                q.add(str);
                data.add(v * vals.get(s + "," + str));
            }
        }
        return -1.0;
    }
    private void init(String[][] equations, double[] values, HashMap<String, List<String>> adj, HashMap<String, Double> vals) {
        for (int i = 0; i < equations.length; i ++) {
            String up = equations[i][0];
            String down = equations[i][1];
            double val = values[i];
            if (!adj.containsKey(up)) {
                adj.put(up, new LinkedList<String>());
            }
            if (!adj.containsKey(down)) {
                adj.put(down, new LinkedList<String>());
            }
            adj.get(up).add(down);
            adj.get(down).add(up);
            vals.put(up + "," + down, val);
            vals.put(down + "," + up, 1/val);
        }
    }
}
```
