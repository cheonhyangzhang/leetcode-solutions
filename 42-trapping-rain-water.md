# 42 Trapping Rain Water

### Problem:
Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it is able to trap after raining.

For example, 
Given [0,1,0,2,1,0,1,3,2,1,2,1], return 6.

![](/assets/rainwatertrap.png)

The above elevation map is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped. Thanks Marcos for contributing this image!

### Solutions:

```java
public class Solution {
    public int trap(int[] height) {
        int left = 0;
        int leftIndex = -1;
        int water = 0;
        int inside = 0;
        HashSet<String> range = new HashSet<String>();
        for (int i = 0; i < height.length; i ++) {
            if (height[i] >= left) {
                range.add(leftIndex+","+i);
                water = water + left * (i - leftIndex - 1) - inside;
                left = height[i];
                leftIndex = i;
                inside = 0;
                
            }
            else {
                inside += height[i];
            }
        }
        int right = 0;
        int rightIndex = height.length;
        inside = 0;
        for (int i = height.length - 1; i >= 0; i --) {
            if (height[i] >= right) {
                if (!range.contains(i+","+rightIndex)) {
                    water = water + right * (rightIndex - i - 1) - inside;
                }
                right = height[i];
                rightIndex = i;
                inside = 0;
            }
            else {
                inside += height[i];
            }
        }
        return water;
    }
}
```