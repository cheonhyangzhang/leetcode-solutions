# 228 Summary Ranges – Medium

### Problem:
Given a sorted integer array without duplicates, return the summary of its ranges.

For example, given [0,1,2,4,5,7], return [“0->2″,”4->5″,”7”].

### Thoughts:
This problem is similar to the missing ranges but this one is easier because there is no trouble of Integer Overflow problem.

In my solution, I use two for loop nested but actually it’s only O(n) time. Because i is skipping the index that j has visited.

So it can be done by using only one loop.

### Solutions:

```java

```