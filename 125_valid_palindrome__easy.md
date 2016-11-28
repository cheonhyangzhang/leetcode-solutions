# 125 Valid Palindrome – Easy


### Problem:



Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

For example,
"A man, a plan, a canal: Panama" is a palindrome.
"race a car" is not a palindrome.

Note:
Have you consider that the string might be empty? This is a good question to ask during an interview.

For the purpose of this problem, we define empty string as valid palindrome.


### Thoughts:



This is just a very basic string manipulation problem. Iteration of String.


### Solutions:



```java
public class Solution {
    public boolean isPalindrome(String s) {
        if (s == null || s.equals("")){
            return true;
        }
        s = s.toLowerCase();
        s = s.replaceAll("[^A-Za-z0-9]","");
        int i = 0;
        int j = s.length() -1;
        for (; i < j; i ++, j --){
            if (s.charAt(i) != s.charAt(j)){
                return false;
            }
        }
        return true;
    }//isPalindrome
}
```
Updated: 11/28/2016
Alternative solution:

```java
public class Solution {
    public boolean isPalindrome(String s) {
        s = s.toLowerCase();
        boolean result = true;
        int i = 0, j = s.length() - 1;
        while (i < j) {
            if (!((s.charAt(i) >= 'a' && s.charAt(i) <= 'z') || (s.charAt(i) >= '0' && s.charAt(i) <= '9'))) {
                i ++;
                continue;
            }
            if (!((s.charAt(j) >= 'a' && s.charAt(j) <= 'z') || (s.charAt(j) >= '0' && s.charAt(j) <= '9'))) {
                j --;
                continue;
            }
            if (s.charAt(i) != s.charAt(j)) {
                result = false;
                break;
            }
            i ++;
            j --;
        }
        return result;
    }
}
```