# 214. Shortest Palindrome

### Problem:

Given a string S, you are allowed to convert it to a palindrome by adding characters in front of it. Find and return the shortest palindrome you can find by performing this transformation.

For example:

Given "aacecaaa", return "aaacecaaa".

Given "abcd", return "dcbabcd".

### Solutions:

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

···java
public class Solution {
    public String shortestPalindrome(String s) {
        if (s.equals("")) {
            return "";
        }
        char[] str = s.toCharArray();
        int left = (s.length() - 1) / 2;
        int right = s.length() / 2;
        int mid1 = 0;
        int mid2 = 0;
        while (left >= 0) {
            int i = left;
            int j = right;
            while (i >= 0 && str[i] == str[j]) {
                i --;
                j ++;
            }
            if (i == -1) {
                mid1 = left;
                mid2 = right;
                break;
            }
            if (left == right) {
                left --;
            }
            else {
                right --;
            }
        }
        String second = s.substring(mid2);
        
        String first = new StringBuilder(second).reverse().toString();
        if (mid1 == mid2) {
            first = first.substring(0, first.length() - 1);
        }
        return first + second;
    }
}
```

```java

```