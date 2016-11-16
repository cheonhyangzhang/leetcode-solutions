# 11 LeetCode Java: Container With Most Water – Medium


### Problem:



Given n non-negative integers a1, a2, …, an, where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

Note: You may not slant the container.


### Thoughts:



The key idea here is that , for any container, the water it could contain is determined by the shorter height. Try candidate from the far left and far right. Always move the shorter pointer to the center.


### Solutions:


```java
public class Solution {
    public int maxArea(int[] height) {
        int left = 0, right = height.length -1;
        int max = 0;
        while (left < right) {
            max = Math.max(max, Math.min(height[left], height[right]) * (right - left));
            if (height[left] < height[right]) {
                left ++;
            }
            else {
                right --;
            }
        }
        return max;
    }
}
```