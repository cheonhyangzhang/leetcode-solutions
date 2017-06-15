# 475. Heaters

### Problem:
Winter is coming! Your first job during the contest is to design a standard heater with fixed warm radius to warm all the houses.

Now, you are given positions of houses and heaters on a horizontal line, find out minimum radius of heaters so that all houses could be covered by those heaters.

So, your input will be the positions of houses and heaters seperately, and your expected output will be the minimum radius standard of heaters.

Note:

1. Numbers of houses and heaters you are given are non-negative and will not exceed 25000.
2. Positions of houses and heaters you are given are non-negative and will not exceed 10^9.
3. As long as a house is in the heaters' warm radius range, it can be warmed.
4. All the heaters follow your radius standard and the warm radius will the same.

Example 1:
```
Input: [1,2,3],[2]
Output: 1
Explanation: The only heater was placed in the position 2, and if we use the radius 1 standard, then all the houses can be warmed.
```

Example 2:
```
Input: [1,2,3,4],[1,4]
Output: 1
Explanation: The two heater was placed in the position 1 and 4. We need to use radius 1 standard, then all the houses can be warmed.
```

### Solutions:

```java
public class Solution {
    public int findRadius(int[] houses, int[] heaters) {
        Arrays.sort(houses);
        Arrays.sort(heaters);
        int max = Integer.MIN_VALUE;
        int left = Integer.MIN_VALUE;
        int right = heaters[0];
        int i = 0, j = 0;
        while (i < houses.length) {
            if (houses[i] >= left && houses[i] <= right) {
                max = Math.max(max, Math.min(left == Integer.MIN_VALUE?Integer.MAX_VALUE : houses[i] - left, right - houses[i]));
                i ++;
            }
            else {
                left = right;
                j ++;
                if (j == heaters.length) {
                    right = Integer.MAX_VALUE;
                }
                else {
                    right = heaters[j];
                }
            }
        }
        return max;
    }
}
```