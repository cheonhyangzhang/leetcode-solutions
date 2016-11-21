# 38 Count and Say – Easy


### Problem:



The count-and-say sequence is the sequence of integers beginning as follows:
1, 11, 21, 1211, 111221, ...

1 is read off as "one 1" or 11.
11 is read off as "two 1s" or 21.
21 is read off as "one 2, then one 1" or 1211.

Given an integer n, generate the nth sequence.

Note: The sequence of integers will be represented as a string.


### Thoughts:



The idea is very straight forward.


### Solutions:


```java
public class Solution {
    public String countAndSay(int n) {
        String result = "";
        for (int i = 0; i < n; i++) {
            if (i == 0) {
                result = "1";
                continue;
            }
            result = process(result);
        }
        return result;
    }
    private String process(String s) {
        String result = "";
        char curr = s.charAt(0);
        int count = 1;
        for (int i = 1; i < s.length(); i ++) {
            if (s.charAt(i) != curr) {
                result += (count + "") + curr;
                curr = s.charAt(i);
                count = 1;
                continue;
            }
            count ++;
        }
        result += (count + "" )+ curr;
        return result;
    }
}
```