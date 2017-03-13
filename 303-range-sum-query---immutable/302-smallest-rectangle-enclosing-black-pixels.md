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