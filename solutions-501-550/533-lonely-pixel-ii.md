# 533 Lonely Pixel II

### Problem:

Given a picture consisting of black and white pixels, and a positive integer N, find the number of black pixels located at some specific row R and column C that align with all the following rules:

Row R and column C both contain exactly N black pixels.
For all rows that have a black pixel at column C, they should be exactly the same as row R
The picture is represented by a 2D char array consisting of 'B' and 'W', which means black and white pixels respectively.

Example:
```
Input:                                            
[['W', 'B', 'W', 'B', 'B', 'W'],    
 ['W', 'B', 'W', 'B', 'B', 'W'],    
 ['W', 'B', 'W', 'B', 'B', 'W'],    
 ['W', 'W', 'B', 'W', 'B', 'W']] 

N = 3
Output: 6
Explanation: All the bold 'B' are the black pixels we need (all 'B's at column 1 and 3).
        0    1    2    3    4    5         column index                                            
0    [['W', 'B', 'W', 'B', 'B', 'W'],    
1     ['W', 'B', 'W', 'B', 'B', 'W'],    
2     ['W', 'B', 'W', 'B', 'B', 'W'],    
3     ['W', 'W', 'B', 'W', 'B', 'W']]    
row index

Take 'B' at row R = 0 and column C = 1 as an example:
Rule 1, row R = 0 and column C = 1 both have exactly N = 3 black pixels. 
Rule 2, the rows have black pixel at column C = 1 are row 0, row 1 and row 2. They are exactly the same as row R = 0.
```

Note:
1. The range of width and height of the input 2D array is [1,200].

### Solutions:

```java
public class Solution {
    public int findBlackPixel(char[][] picture, int N) {
        char[][] pic = picture;
        if (pic == null || pic.length == 0 || pic[0].length == 0) {
            return 0;
        }
        int[] row = new int[pic.length];
        int[] col = new int[pic[0].length];
        for (int i = 0; i < pic.length; i ++) {
            for (int j = 0; j < pic[0].length; j ++) {
                if (pic[i][j] == 'B') {
                    row[i] ++;
                    col[j] ++;
                }
            }
        }
        HashMap<String, List<Integer>> rows = new HashMap<String, List<Integer>>();
        for (int i = 0; i < pic.length; i ++) {
            if (row[i] != N) {
                continue;
            }
            String arow = new String(pic[i]);
            if (!rows.containsKey(arow)) {
                rows.put(arow, new LinkedList<Integer>());
            }
            rows.get(arow).add(i);
        }
        int count = 0;
        for (String key:rows.keySet()) {
            List<Integer> rowIndex = rows.get(key);
            int selected = rowIndex.size();
            if (selected != N) {
                continue;
            }
            int i = rowIndex.get(0);
            int add = 0;
            for (int j = 0; j < pic[0].length; j ++) {
                if (pic[i][j] != 'B') {
                    continue;
                }
                int total = col[j];
                if (total != selected) {
                    continue;
                }
                add ++;
            }
            count += add * selected;
        }
        return count;
    }
}
```