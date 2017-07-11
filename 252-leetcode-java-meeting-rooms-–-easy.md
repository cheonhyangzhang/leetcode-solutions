# 252 Meeting Rooms II – Easy

### Problem:

Given an array of meeting time intervals consisting of start and end times [[s1,e1],[s2,e2],…] (si < ei), determine if a person could attend all meetings.

For example,
Given [[0, 30],[5, 10],[15, 20]],
return false.

### Thoughts:

We can solve this problem easily by sorting the Intervals. But there is no custom comparator for it so that we need to create one.

We want to sort the Interval by the start time, then if a person can attend all meetings, the start time of a meeting must be after the end time of the previous one.

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
    class IntervalComparator implements Comparator<Interval> {
        @Override
        public int compare(Interval i1, Interval i2) {
            if (i1.start > i2.start) {
                return 1;
            }
            else if (i1.start < i2.start) {
                return -1;
            }
            else {
                return 0;
            }
        }
    } 
    public boolean canAttendMeetings(Interval[] intervals) {
        Arrays.sort(intervals, new IntervalComparator());
        for (int i = 1; i < intervals.length; i ++) {
            if (intervals[i].start < intervals[i-1].end) {
                return false;
            }
        }
        return true;
    }
}
```