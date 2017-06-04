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
        HashMap<String, List<String>> flights = new HashMap<String, List<String>>();
        List<String> remain = new LinkedList<String>();
        for (int i = 0; i < tickets.length; i ++) {
            if (!flights.containsKey(tickets[i][0])) {
                flights.put(tickets[i][0], new LinkedList<String>());
            }
            flights.get(tickets[i][0]).add(tickets[i][1]);
            remain.add(tickets[i][0] + tickets[i][1]);
        }
        for (String c:flights.keySet()) {
            Collections.sort(flights.get(c));
        }
        return fi(tickets.length + 1, "JFK", flights, new LinkedList<String>(), remain);
    }
    private List<String> fi(int n, String port, HashMap<String, List<String>> flights, List<String> curr, List<String> remain) {
        curr.add(port);
        if (curr.size() == n) {
            return new LinkedList<String>(curr);
        }
        if (flights.containsKey(port)) {
            for (String next:flights.get(port)) {
                if (!remain.contains(port + next)) {
                    continue;
                }
                remain.remove(port + next);
                List<String> result = fi(n, next, flights, curr, remain);
                if (result != null) {
                    return result;
                }
                remain.add(port + next);
            }   
        }
        curr.remove(curr.size() - 1);
        return null;
    }
}
```

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
        fi(result, "JFK", flights);
        return result;
    }
    private void fi(List<String> result, String port, HashMap<String, PriorityQueue<String>> flights) {
        PriorityQueue<String> q = flights.get(port);
        while (q != null && !q.isEmpty()) {
            fi(result, q.poll(), flights);
        }
        result.add(0, port);
    }
}
```