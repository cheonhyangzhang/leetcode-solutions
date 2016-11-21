# 70 Climbing Stairs – Easy


### Problem:



You are climbing a stair case. It takes n steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?


### Thoughts:



Very straight forward solution.

ways[i] = ways[i-1] + ways[i-2];

### Solutions:


```java
public class Solution {
    public int climbStairs(int n) {
        int prepre = 0, pre = 1;
        for (int i = 0; i < n; i ++) {
            int tmp = prepre + pre;
            prepre = pre;
            pre = tmp;
        }
        return pre;
    }//climb
}
```