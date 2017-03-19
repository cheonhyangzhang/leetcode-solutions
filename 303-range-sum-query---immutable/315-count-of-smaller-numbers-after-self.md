# 315 Count of Smaller Numbers After Self

### Problem:
You are given an integer array nums and you have to return a new counts array. The counts array has the property where counts[i] is the number of smaller elements to the right of nums[i].

Example:
```
Given nums = [5, 2, 6, 1]

To the right of 5 there are 2 smaller elements (2 and 1).
To the right of 2 there is only 1 smaller element (1).
To the right of 6 there is 1 smaller element (1).
To the right of 1 there is 0 smaller element.
```

Return the array [2, 1, 1, 0].

### Solutions:

Binary search insert

```java
public class Solution {
    public List<Integer> countSmaller(int[] nums) {
        List<Integer> result = new LinkedList<Integer>();
        ArrayList<Integer> cand = new ArrayList<Integer>();
        for (int i = nums.length - 1; i >= 0; i --) {
            int left = 0, right = cand.size();
            while(left < right) {
                int mid = (right - left) / 2 + left;
                if (cand.get(mid) < nums[i]) {
                    left = mid + 1;
                }
                else {
                    right = mid;
                }
            }
            result.add(0, right);
            cand.add(right, nums[i]);
        }
        return result;
    }
}
```

