# 531 Lonely Pixel I
Given a picture consisting of black and white pixels, find the number of black lonely pixels.

The picture is represented by a 2D char array consisting of 'B' and 'W', which means black and white pixels respectively.

A black lonely pixel is character 'B' that located at a specific position where the same row and same column don't have any other black pixels.

Example:
```
Input: 
[['W', 'W', 'B'],
 ['W', 'B', 'W'],
 ['B', 'W', 'W']]

Output: 3
Explanation: All the three 'B's are black lonely pixels.
```
Note:
1. The range of width and height of the input 2D array is [1,500].

### Solutions:

```java
public class Solution {
    public int findLonelyPixel(char[][] picture) {
        if (picture == null || picture.length == 0 || picture[0].length == 0) {
            return 0;
        }
        int[] row = new int[picture.length];
        int[] column = new int[picture[0].length];
        for (int i = 0; i < picture.length; i ++) {
            for (int j = 0; j < picture[0].length; j ++) {
                if (picture[i][j] == 'B') {
                    row[i] ++;
                    column[j] ++;
                }
            }
        }
        int count = 0;
        for (int i = 0; i < picture.length; i ++) {
            for (int j = 0; j < picture[0].length; j ++) {
                if (picture[i][j] == 'B' && row[i] == 1 && column[j] == 1) {
                    count ++;
                }
            }
        }
        return count;
    }
}
```