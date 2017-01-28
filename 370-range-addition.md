# 370 Range Addition

### Problem:

Assume you have an array of length n initialized with all 0's and are given k update operations.

Each operation is represented as a triplet: [startIndex, endIndex, inc] which increments each element of subarray A[startIndex ... endIndex] (startIndex and endIndex inclusive) with inc.

Return the modified array after all k operations were executed.

Hint:
Thinking of using advanced data structures? You are thinking it too complicated.
For each update operation, do you really need to update all elements between i and j?
Update only the first and end element is sufficient.
The optimal time complexity is O(k + n) and uses O(1) extra space.


Example:
```
Given:

    length = 5,
    updates = [
        [1,  3,  2],
        [2,  4,  3],
        [0,  2, -2]
    ]

Output:

    [-2, 0, 3, 5, 3]
```

Explanation:
```
Initial state:
[ 0, 0, 0, 0, 0 ]

After applying operation [1, 3, 2]:
[ 0, 2, 2, 2, 0 ]

After applying operation [2, 4, 3]:
[ 0, 2, 5, 5, 3 ]

After applying operation [0, 2, -2]:
[-2, 0, 3, 5, 3 ]
```

```java
public class Solution {
    public int[] getModifiedArray(int length, int[][] updates) {
        int[] result = new int[length];
        for (int i = 0; i < updates.length; i ++) {
            result[updates[i][0]] += updates[i][2];
            if (updates[i][1] + 1 < length) {
                result[updates[i][1] + 1] -= updates[i][2];
            }
        }
        int curr = 0;
        for (int i = 0; i < result.length; i ++) {
            if (result[i] != 0) {
                curr += result[i];
            }
            result[i] = curr;
        }
        return result;
    }
}
```