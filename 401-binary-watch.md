# 401 Binary Watch

### Problem:

A binary watch has 4 LEDs on the top which represent the hours (0-11), and the 6 LEDs on the bottom represent the minutes (0-59).
![](/assets/Binary_clock_samui_moon.jpg)
Each LED represents a zero or one, with the least significant bit on the right.

For example, the above binary watch reads "3:25".

Given a non-negative integer n which represents the number of LEDs that are currently on, return all possible times the watch could represent.

Example:
```
Input: n = 1
Return: ["1:00", "2:00", "4:00", "8:00", "0:01", "0:02", "0:04", "0:08", "0:16", "0:32"]
```

Note:
* The order of output does not matter.
* The hour must not contain a leading zero, for example "01:00" is not valid, it should be "1:00".
* The minute must be consist of two digits and may contain a leading zero, for example "10:2" is not valid, it should be "10:02".

### Solutions:

```java
public class Solution {
    public List<String> readBinaryWatch(int num) {
        boolean[] watch = new boolean[10];
        int[] vals = new int[]{8, 4, 2, 1, 32, 16, 8, 4, 2, 1};
        List<String> result = new LinkedList<String>();
        process(num, 0, watch, vals, result);
        return result;
    }
    private void process(int left, int start, boolean[] watch, int[] vals, List<String> result) {
        if (left == 0) {
            int hour = 0;
            for (int i = 0; i < 4; i ++) {
                if (watch[i] == true) {
                    hour += vals[i];
                }
            }
            if (hour >= 12) {
                return;
            }
            int min = 0;
            for (int i = 4; i < 10; i ++) {
                if (watch[i] == true) {
                    min += vals[i];
                }
            }
            if (min >= 60) {
                return;
            }
            String time = hour + ":";
            if (min < 10) {
                time += "0";
            }
            time +=min;
            result.add(0, time);
            return;
        }
        for (int i = start; i< watch.length; i ++) {
            watch[i] = true;
            process(left - 1, i + 1, watch, vals, result);
            watch[i] = false;
        }
    }
}
```