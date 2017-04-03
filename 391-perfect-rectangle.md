# 391. Perfect Rectangle

### Problem:

Given N axis-aligned rectangles where N > 0, determine if they all together form an exact cover of a rectangular region.

Each rectangle is represented as a bottom-left point and a top-right point. For example, a unit square is represented as [1,1,2,2]. (coordinate of bottom-left point is (1, 1) and top-right point is (2, 2)).


Example 1:
```
rectangles = [
  [1,1,3,3],
  [3,1,4,2],
  [3,2,4,4],
  [1,3,2,4],
  [2,3,3,4]
]

Return true. All 5 rectangles together form an exact cover of a rectangular region.
```
![](/assets/rectangle_perfect.gif)
Example 2:
```
rectangles = [
  [1,1,2,3],
  [1,3,2,4],
  [3,1,4,2],
  [3,2,4,4]
]

Return false. Because there is a gap between the two rectangular regions.
```
![](/assets/rectangle_separated.gif)
Example 3:
```
rectangles = [
  [1,1,3,3],
  [3,1,4,2],
  [1,3,2,4],
  [3,2,4,4]
]

Return false. Because there is a gap in the top center.
```
![](/assets/rectangle_hole.gif)
Example 4:
```
rectangles = [
  [1,1,3,3],
  [3,1,4,2],
  [1,3,2,4],
  [2,2,4,4]
]

Return false. Because two of the rectangles overlap with each other.
```
![](/assets/rectangle_intersect.gif)


### Solutions:
Not working solution
```java
public class Solution {
    public boolean isRectangleCover(int[][] rectangles) {
        int blox = Integer.MAX_VALUE, bloy = Integer.MAX_VALUE, trix = Integer.MIN_VALUE, triy = Integer.MIN_VALUE;
        for (int i = 0; i < rectangles.length; i ++) {
            int[] rect = rectangles[i];
            if (!(rect[0] > blox || rect[1] > bloy)) {
                blox = rect[0];
                bloy = rect[1];
            }
            if (!(rect[2] < trix || rect[3] < triy)) {
                trix = rect[2];
                triy = rect[3];
            }
        }
        
        System.out.println(blox + ", " + bloy + " : " + trix + ", " + triy);
        boolean[][] covered = new boolean[trix - blox][triy - bloy];
        for (int i = 0; i < rectangles.length; i ++) {
            int[] rect = rectangles[i];
            for (int m = rect[0] - blox; m < rect[2] - blox; m ++) {
                for (int n = rect[1] - bloy; n < rect[3] - bloy; n ++) {
                    if (m < 0 || m >= covered.length || n < 0 || n >= covered[0].length) {
                        System.out.println("out of bound");
                        return false;
                    }
                    if (covered[m][n] == true) {
                        return false;
                    }
                    covered[m][n] = true;
                }
            }
        }
        for (int i = 0; i < covered.length; i ++) {
            for (int j = 0; j < covered[0].length; j ++) {
                if (covered[i][j] == false) {
                    return false;
                }
            }
        }
        return true;
    }
}
```

```java

```