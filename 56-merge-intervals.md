# 56 Merge Intervals

### Problem:

Given a collection of intervals, merge all overlapping intervals.

For example,
Given [1,3],[2,6],[8,10],[15,18],
return [1,6],[8,10],[15,18].

### Solutions:

```java
/**
 * Definition for an interval.
 * public class Interval {
 *     int start;
 *     int end;
 *     Interval() { start = 0; end = 0; }
 *     Interval(int s, int e) { start = s; end = e; }
 * }
 */
public class Solution {
    public List<Interval> merge(List<Interval> intervals) {
        Collections.sort(intervals, new Comparator<Interval>(){
            public int compare(Interval i1, Interval i2) {
                if (i1.start != i2.start) {
                    return i1.start - i2.start;
                }
                else {
                    return i1.end - i2.end;
                }
            }
        });
        List<Interval> result = new LinkedList<Interval>();
        Interval curr = null;
        for (Interval inter:intervals) {
            if (curr == null) {
                curr = inter;
                continue;
            }
            if (inter.start > curr.end) {
                result.add(curr);
                curr = inter;
            }
            else {
                curr.end = Math.max(curr.end, inter.end);
            }
        }
        if (curr != null) {
            result.add(curr);
        }
        return result;
    }
}
```