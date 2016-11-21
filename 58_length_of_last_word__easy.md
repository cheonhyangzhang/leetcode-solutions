# 58 Length of Last Word – Easy


### Problem:



Given a string s consists of upper/lower-case alphabets and empty space characters ' ', return the length of last word in the string.

If the last word does not exist, return 0.

Note: A word is defined as a character sequence consists of non-space characters only.

For example,
Given s = "Hello World",
return 5.


### Thoughts:



String manipulation. Too straight forward. No need to explain.


### Solutions:



```java
public class Solution {
    public int lengthOfLastWord(String s) {
        int len = 0;
        s = s.trim();
        for (int i = s.length() - 1; i >=0; i --){
            if (s.charAt(i) == ' '){
                break;
            }
            else{
                len ++;
            }
        }
        return len;
    }
}
```
Alternative solution:
```java
public class Solution {
    public int lengthOfLastWord(String s) {
        int i = s.length() -1;
        int len = 0;
        while (i >=0 && s.charAt(i) == ' ') {
            i --;
        }
        while (i >=0) {
            if (s.charAt(i) == ' ') {
                break;
            }
            i --; len ++;
        }
        return len;
    }
}
```