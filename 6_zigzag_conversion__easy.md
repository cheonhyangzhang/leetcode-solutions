# 6 ZigZag Conversion – Easy


### Problem:


The string “PAYPALISHIRING” is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

P A H N
A P L S I I G
Y I R
And then read line by line: “PAHNAPLSIIGYIR”
Write the code that will take a string and make this conversion given a number of rows:

string convert(string text, int nRows);
convert(“PAYPALISHIRING”, 3) should return “PAHNAPLSIIGYIR”.


### Thoughts:



Use a delta flag to indicate whether next move should go up or go down.

### Solutions:



```java
public class Solution {
    public String convert(String s, int nRows) {
        String[] helper = new String[nRows];
        for (int i = 0; i < nRows; i ++){
            helper[i] = "";
        }
        int row = 0;
        int delta = 1;
        for (int i = 0; i < s.length(); i ++){
            char c = s.charAt(i);
            helper[row] += c;
            if (row == nRows - 1){
                delta = -1;
            }
            else if (row == 0){
                delta = 1;
            }
            row = row + delta;
            row = Math.max(0, row);
        }//for
        String result = "";
        for (int i = 0; i < nRows && s.length() > 0; i ++){
            result += helper[i];
        }
        return result;
    }
}
```