# 551. Student Attendance Record I

### Problem:
You are given a string representing an attendance record for a student. The record only contains the following three characters:

'A' : Absent.
'L' : Late.
'P' : Present.
A student could be rewarded if his attendance record doesn't contain more than one 'A' (absent) or more than two continuous 'L' (late).

You need to return whether the student could be rewarded according to his attendance record.

Example 1:
```
Input: "PPALLP"
Output: True
```
Example 2:
```
Input: "PPALLL"
Output: False
```

### Solutions:

```java
public class Solution {
    public boolean checkRecord(String s) {
        boolean hasA = false;
        int countL = 0;
        for (int i = 0; i < s.length(); i ++) {
            char c = s.charAt(i);
            if (c == 'A') {
                if (hasA == true) {
                    return false;
                }
                hasA = true;
            }
            if (c == 'L') {
                countL ++;
                if (countL == 3) {
                    return false;
                }
            }
            else {
                countL = 0;
            }
        }
        return true;
    }
}
```


```java
public class Solution {
    public boolean checkRecord(String s) {
        return !s.matches(".*A.*A.*|.*LLL.*");
    }
}
```