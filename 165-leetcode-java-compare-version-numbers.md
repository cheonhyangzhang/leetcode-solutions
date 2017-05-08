# 165 LeetCode Java: Compare Version Numbers 

### Problem:
Compare two version numbers version1 and version2.
If version1 > version2 return 1, if version1 < version2 return -1, otherwise return 0.

You may assume that the version strings are non-empty and contain only digits and the . character.
The . character does not represent a decimal point and is used to separate number sequences.
For instance, 2.5 is not “two and a half” or “half way to version three”, it is the fifth second-level revision of the second first-level revision.

Here is an example of version numbers ordering:
```
0.1 < 1.1 < 1.2 < 13.37
```

### Thoughts:
The very first trick is to split the String by “.” into tokens.

Then compare two array until reach the end or already has a winner.

The purpose of this problem is on figuring out all different cases, including edge cases.

You don’t know how many levels in total for a version number. So 1.3.2.4.5.6 is also possible, it’s not common in practical world, but it’s a valid version number in this problem.

Also. you could have ending 0, e.g. 1.0 and 1.
Remember to use the escape for the “.”, which is “\\.” in regex in Java.

### Solutions:

```java
public class Solution {
    public int compareVersion(String version1, String version2) {
        String[] v1 = version1.split("\\.");
        String[] v2 = version2.split("\\.");
        int i = 0;
        for (i = 0; i < v1.length && i < v2.length; i ++){ 
            int d1 = Integer.parseInt(v1[i]); 
            int d2 = Integer.parseInt(v2[i]); 
            if (d1 > d2)
                return 1;
            else if (d1 < d2)
                return -1;
        }//for i
        if (i == v1.length && i == v2.length){
            return 0;
        }
        else if (i == v1.length){
            for (int j = i; j < v2.length; j ++){
                if (Integer.parseInt(v2[j]) !=0)
                    return -1;
            }
            return 0;
        }
        else if (i == v2.length){
            for (int j = i; j < v1.length; j ++){
                if (Integer.parseInt(v1[j]) !=0)
                    return 1;
            }
            return 0;
        }
        else{
            return -2;
        }
    }//compareVersion
}
```
#### Updated: 12/27/2016
Improve logic:
```java
public class Solution {
    public int compareVersion(String version1, String version2) {
        String[] v1s = version1.split("\\.");
        String[] v2s = version2.split("\\.");
        int i = 0;
        for (; i < v1s.length && i < v2s.length; i ++) {
            int v1 = Integer.parseInt(v1s[i]);
            int v2 = Integer.parseInt(v2s[i]);
            if (v1 > v2) {
                return 1;
            }
            if (v2 > v1) {
                return -1;
            }
        }
        if (i < v1s.length) {
            for (;i < v1s.length;i++) {
                if (Integer.parseInt(v1s[i]) != 0) {
                    return 1;
                }
            }
        }
        if (i < v2s.length) {
            for (;i < v2s.length;i++) {
                if (Integer.parseInt(v2s[i]) != 0) {
                    return -1;
                }
            }
        }
        return 0;
    }
}
```