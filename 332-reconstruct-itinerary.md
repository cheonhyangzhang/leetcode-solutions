# 332. Reconstruct Itinerary

### Problem:

<pre>
Given a list of airline tickets represented by pairs of departure and arrival airports [from, to], reconstruct the itinerary in order. All of the tickets belong to a man who departs from JFK. Thus, the itinerary must begin with JFK.

Note:
If there are multiple valid itineraries, you should return the itinerary that has the smallest lexical order when read as a single string. For example, the itinerary ["JFK", "LGA"] has a smaller lexical order than ["JFK", "LGB"].
All airports are represented by three capital letters (IATA code).
You may assume all tickets form at least one valid itinerary.
Example 1:
tickets = [["MUC", "LHR"], ["JFK", "MUC"], ["SFO", "SJC"], ["LHR", "SFO"]]
Return ["JFK", "MUC", "LHR", "SFO", "SJC"].
Example 2:
tickets = [["JFK","SFO"],["JFK","ATL"],["SFO","ATL"],["ATL","JFK"],["ATL","SFO"]]
Return ["JFK","ATL","JFK","SFO","ATL","SFO"].
Another possible reconstruction is ["JFK","SFO","ATL","JFK","ATL","SFO"]. But it is larger in lexical order.
</pre>

### Solutions:

```java
public class Solution {
    public List<String> findItinerary(String[][] tickets) {
        HashMap<String, PriorityQueue<String>> flights = new HashMap<String, PriorityQueue<String>>();
        for (int i = 0; i < tickets.length; i ++) {
            if (!flights.containsKey(tickets[i][0])) {
                flights.put(tickets[i][0], new PriorityQueue<String>());
            }
            flights.get(tickets[i][0]).add(tickets[i][1]);
        }
        List<String> result = new LinkedList<String>();
        result.add("JFK");
        fi(tickets.length + 1, result, "JFK", flights);
        return result;
    }
    private boolean fi(int n, List<String> result, String port, HashMap<String, PriorityQueue<String>> flights) {
        if (result.size() == n) {
            return true;
        }
        PriorityQueue<String> q = flights.get(port);
        while (q != null && !q.isEmpty()) {
            String s = q.poll();
            result.add(s);
            boolean finished = fi(n, result, s, flights);
            if (finished == true) {
                return true;
            }
            result.remove(result.size() - 1);
            q.add(s);
        }
        return false;
    }
}
```