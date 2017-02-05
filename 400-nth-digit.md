# 400 Nth Digit

### Problem:

Find the nth digit of the infinite integer sequence 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, ...

Note:
n is positive and will fit within the range of a 32-bit signed integer (n < 231).

Example 1:
```
Input:
3

Output:
3
```

Example 2:
```
Input:
11

Output:
0

Explanation:
The 11th digit of the sequence 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, ... is a 0, which is part of the number 10.
```

# Solutions:

```java
public class Solution {
    public int findNthDigit(int n) {
        long base = 9;
        int width = 1;
        long count = 0; //number of digits already before the start the the range
        int start = 1; //start number of the range
        while (n > count + base * width) {
            count += base * width;
            base = base * 10;
            width ++;
            start = start * 10;            
        }
        int diff = (int)(n - count - 1);
        int number = start + diff / width;
        int offset = width - diff % width - 1;
        for (int i = 0; i < offset; i ++) {
            number = number / 10;
        }
        return number % 10;
    }
}
```