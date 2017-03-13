# 302. Smallest Rectangle Enclosing Black Pixels

### Problem:

An image is represented by a binary matrix with 0 as a white pixel and 1 as a black pixel. The black pixels are connected, i.e., there is only one black region. Pixels are connected horizontally and vertically. Given the location (x, y) of one of the black pixels, return the area of the smallest (axis-aligned) rectangle that encloses all black pixels.

For example, given the following image:

```
[
  "0010",
  "0110",
  "0100"
]
```
and x = 0, y = 2,
Return 6.

### Solutions:

```java
public class Solution {
    public int minArea(char[][] image, int x, int y) {
        if (image == null || image.length == 0) {
            return 0;
        }
        int m = image.length, n = image[0].length;
        int[] border = new int[] {m, -1, n, -1};
        dfs(image, x, y, border);
        return (border[1] - border[0] + 1) * (border[3] - border[2] + 1);
    }
    private void dfs(char[][] image, int x, int y, int[] border) {
        if (x < 0 || x >= image.length || y < 0 || y >= image[0].length || image[x][y] != '1') {
            return;
        }
        border[0] = Math.min(border[0], x);
        border[1] = Math.max(border[1], x);
        border[2] = Math.min(border[2], y);
        border[3] = Math.max(border[3], y);
        image[x][y] = '2';
        dfs(image, x - 1, y, border);
        dfs(image, x, y - 1, border);
        dfs(image, x + 1, y, border);
        dfs(image, x, y + 1, border);
    }
}
```

```java
public class Solution {
    public int minArea(char[][] image, int x, int y) {
        if (image == null || image.length == 0) {
            return 0;
        }
        int m = image.length, n = image[0].length;
        int up = bs(image, false, true, 0, x, 0, n);
        int down = bs(image, true, true, x + 1, m, 0, n);
        int left = bs(image, false, false, 0, y, up, down);
        int right = bs(image, true, false, y + 1, n, up, down);
        return (down - up) * (right - left);
    }
    // incOnOne to indicate if looking for lower border or upper border
    private int bs(char[][] image, boolean incOnOne, boolean vertical, int low, int high, int rangeStart, int rangeEnd) {
        while (low < high) {
            int mid = (high - low) / 2 + low;
            boolean hasOne = false;
            for (int j = rangeStart; j < rangeEnd; j ++) {
                char c = '#';
                if (vertical) {
                    c = image[mid][j];
                }
                else {
                    c = image[j][mid];
                }
                if (c == '1') {
                    hasOne = true;
                    break;
                }
            }
            if (hasOne) {
                if (incOnOne) {
                    low = mid + 1;
                }
                else {
                    high = mid;
                }
            }
            else {
                if (incOnOne) {
                    high = mid;
                }
                else {
                    low = mid + 1;
                }
            }
        }
        return low;
    }
}
```