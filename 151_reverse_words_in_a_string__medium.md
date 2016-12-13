# 151 Reverse Words in a String – Medium


### Problem:



Given an input string, reverse the string word by word.

For example,
Given s = “the sky is blue“,
return “blue is sky the“.


### Thoughts:



This looks like a very simple problem.

Using Java’s String’s split method into a String array. It is super easy to solve the problem.

I am not very sure what’s the purpose of this problem.

Below is using another approach which is more String manipulation way, iterating characters in String.


### Solutions:



```java
public class Solution {
    public String reverseWords(String s) {
        if (s == null)
            return null;
        s = s.trim();
        String result = "";
        String word = "";
        for (int i = 0; i < s.length(); i ++){
            if (s.charAt(i) == ' '){
                while (s.charAt(i) == ' ')
                    i ++;
                result = " " + word + result;
                word = "" + s.charAt(i);
            }
            else{
                word +=s.charAt(i);
            }
        }
        result = word + result;
        return result;
    }
}
```
Updated: 12/12/2016
Alternative solution.

```java
public class Solution {
    public String reverseWords(String s) {
        int i = 0;
        String result = "";
        while (i < s.length()) {
            if (s.charAt(i) == ' ') {
                i ++;
                continue;
            }
            //generate a world
            String word = "";
            while (i < s.length() && s.charAt(i) != ' ') {
                word += s.charAt(i);
                i ++;
            }
            if (result.equals("")) {
                result = word;
            }
            else {
                result = word + " " + result;
            }
        }
        return result;
    }
}
```
Alternative solution 2.

```java
public class Solution {
    public String reverseWords(String s) {
        String[] strs = s.split(" ");
        String result = "";
        for (int i = 0; i < strs.length; i ++) {
            if (strs[i].equals("")) {
                continue;
            }
            if (result.equals("")) {
                result = strs[i];
            }
            else {
                result = strs[i] + " " + result;
            }
        }
        return result;
    }
}
```