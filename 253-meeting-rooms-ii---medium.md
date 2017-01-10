# 253 LeetCode Java: Meeting Rooms – Medium

### Problem:

Given an array of meeting time intervals consisting of start and end times [[s1,e1],[s2,e2],…] (si < ei), find the minimum number of conference rooms required.

For example,
Given [[0, 30],[5, 10],[15, 20]],
return 2.

### Thoughts:

We still need to sort the intervals by start time in order to make things easier.
A very straightforward way is to have a List of Interval and stored as the occupied interval of a room. And the size of the List will be the number of rooms required.

Because the start time is in increasing order, so that when you found a meeting that needs to be put into one room, it doesn't matter which available room to put in. E.g. if there are three rooms can support a meeting at 1pm and the end time of three rooms are 9 am , 10 am and 11 am. We can arrange this meeting at 1pm to any of the three. Because we know the next (if has next) meeting will start later than 1pm. No matter where we put 1pm meeting, we will have only two rooms available for the later ones.

Because we only care about the end time of a room, so actually we can use a min-heap to keep track of end time so that we don't need to iterate over the list of rooms. Because for a heap. add takes O(logn) in worse case and peek takes O(1) which would be mush faster.

Note that in Java, PriorityQueue is default to be min-heap. If we want to use max-heap, we have to use PriorityQueue pq = new PriorityQueue(11, Collections.reverseOrder());.

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
            return i1.start - i2.start;
        }
    }
    public int minMeetingRooms(Interval[] intervals) {
        List<Interval> rooms = new LinkedList<Interval>();
        if (intervals.length == 0) {
            return 0;
        }
        Arrays.sort(intervals, new IntervalComparator());
        rooms.add(intervals[0]);
        for (int i = 1; i < intervals.length; i ++) {
            boolean found = false;
            for (Interval inter:rooms) {
                if (intervals[i].start >= inter.end) {
                    inter.end = intervals[i].end;
                    found = true;
                    break;
                }
            }
            if (found == false) {
                rooms.add(intervals[i]);
            }
        }
        return rooms.size();
    }
}
```
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
            return i1.start - i2.start;
        }
    }
    public int minMeetingRooms(Interval[] intervals) {
        PriorityQueue<Integer> end = new PriorityQueue<Integer>();
        if (intervals.length == 0) {
            return 0;
        }
        Arrays.sort(intervals, new IntervalComparator());
        end.add(intervals[0].end);
        for (int i = 1; i < intervals.length; i ++) {
            if (intervals[i].start >= end.peek()) {
                end.poll();
            }
            end.add(intervals[i].end);
        }
        return end.size();
    }
}
```
