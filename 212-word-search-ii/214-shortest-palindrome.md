# 214. Shortest Palindrome

### Problem:

Given a string S, you are allowed to convert it to a palindrome by adding characters in front of it. Find and return the shortest palindrome you can find by performing this transformation.

For example:

Given "aacecaaa", return "aaacecaaa".

Given "abcd", return "dcbabcd".

### Solutions:

Easy to understand
```java
public class Solution {
    public String shortestPalindrome(String s) {
        char[] arr = s.toCharArray();
        for (int i = 1; i <= s.length(); i ++) {
            if (isPa(arr, 0, s.length() - i) == true) {
                return new StringBuilder(s.substring(s.length() - i + 1)).reverse().toString() + s;
            }    
        }
        return "";
    }
    private boolean isPa(char[] arr, int start, int end) {
        while (start < end) {
            if (arr[start] != arr[end]) {
                return false;
            }
            start ++;
            end --;
        }
        return true;
    }
}
```

```java
public class Solution {
    public String shortestPalindrome(String s) {
        int i = 0, end = s.length() - 1, j = end;
        char[] arr = s.toCharArray();
        while (i < j) {
            if (arr[i] == arr[j]) {
                ++i; --j;
            } else {
                i = 0; --end; j = end;
            }
        }
        return new StringBuilder(s.substring(end + 1)).reverse().toString() + s;
    }
}
```


```java
public class Solution {
    public String shortestPalindrome(String s) {
        int i=0; 
        int j=s.length()-1;
     
        while(j>=0){
            if(s.charAt(i)==s.charAt(j)){
                i++;
            }
            j--;
        }
     
        if(i==s.length())
            return s;
     
        String suffix = s.substring(i);
        String prefix = new StringBuilder(suffix).reverse().toString();
        String mid = shortestPalindrome(s.substring(0, i));
        return prefix+mid+suffix;
    }
}
```


