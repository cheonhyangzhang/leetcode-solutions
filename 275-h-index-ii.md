# 275. H-Index II

### Problem:

Follow up for H-Index: What if the citations array is sorted in ascending order? Could you optimize your algorithm?

Hint:

Expected runtime complexity is in O(log n) and the input is sorted.

### Solutions:

```java
public class Solution {
    public int hIndex(int[] citations) {
        if (citations.length == 0) {
            return 0;
        }
        int left = 0, right = citations.length - 1;
        while (left <= right) {
            int mid = (left + right) / 2;
            if (citations[mid] < citations.length - mid) {
                left = mid + 1;
            }
            else {
                right = mid - 1;
            }
        }
        return citations.length - left;
    }
}
```