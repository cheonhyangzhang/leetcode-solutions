# 57 Insert Interval

### Problem:

Given a set of non-overlapping intervals, insert a new interval into the intervals (merge if necessary).

You may assume that the intervals were initially sorted according to their start times.

Example 1:
Given intervals [1,3],[6,9], insert and merge [2,5] in as [1,5],[6,9].

Example 2:
Given [1,2],[3,5],[6,7],[8,10],[12,16], insert and merge [4,9] in as [1,2],[3,10],[12,16].

This is because the new interval [4,9] overlaps with [3,5],[6,7],[8,10].

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
    public List<Interval> insert(List<Interval> intervals, Interval newInterval) {
        List<Interval> result = new LinkedList<Interval>();
        for (Interval inter:intervals) {
            if (newInterval.start > inter.end || newInterval.end < inter.start) {
                //no overlap
                result.add(inter);
                continue;
            }
            newInterval.start = Math.min(newInterval.start, inter.start);
            newInterval.end = Math.max(newInterval.end, inter.end);
        }
        int i = 0;
        for (Interval inter:result) {
            if (newInterval.start < inter.start) {
                break;
            }
            i ++;
        }
        if (i < result.size()) {
            result.add(i, newInterval);
        }
        else {
            result.add(newInterval);
        }
        
        return result;
    }
}
```