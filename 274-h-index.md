# 274. H-Index

### Problem:

Given an array of citations (each citation is a non-negative integer) of a researcher, write a function to compute the researcher's h-index.

According to the definition of h-index on Wikipedia: "A scientist has index h if h of his/her N papers have at least h citations each, and the other N − h papers have no more than h citations each."

For example, given citations = [3, 0, 6, 1, 5], which means the researcher has 5 papers in total and each of them had received 3, 0, 6, 1, 5 citations respectively. Since the researcher has 3 papers with at least 3 citations each and the remaining two with no more than 3 citations each, his h-index is 3.

Note: If there are several possible values for h, the maximum one is taken as the h-index.

Hint:

An easy approach is to sort the array first.
What are the possible values of h-index?
A faster approach is to use extra space.

### Solutions:

```java
public class Solution {
    public int hIndex(int[] citations) {
        Arrays.sort(citations);
        for (int i = citations.length; i > 0; i --) {
            if (citations[citations.length - i] >= i) {
                return i;
            }
        }
        return 0;
    }
}
```

```java
public class Solution {
    public int hIndex(int[] citations) {
        int[] stats = new int[citations.length + 1];
        for (int i = 0; i < citations.length; i ++) {
            int n = citations[i];
            n = Math.min(n, citations.length);
            stats[n] ++;
        }
        int sum = 0;
        for (int i = stats.length - 1; i > 0; i --) {
            sum += stats[i];
            if (sum >= i) {
                return i;
            }
        }
        return 0;
    }
}
```
