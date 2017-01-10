# 247 LeetCode Java: Strobogrammatic Number II – Medium

### Problem:

A strobogrammatic number is a number that looks the same when rotated 180 degrees (looked at upside down).

Find all strobogrammatic numbers that are of length = n.

For example,
Given n = 2, return [“11″,”69″,”88″,”96”].

Hint:

Try to use recursion and notice that it should recurse with n – 2 instead of n – 1.

### Thoughts:

This is a expansion of the version I problem. This problem has a obvious hint of divide and conquer. It can be reduced to sub problems.
We are going to build a string of n length, what if we already know the n – 2 length solution to the problem? Then we just surround that by ‘1’ and ‘1’, ‘8’ and ‘8’, ‘6’ and ‘9’ etc.
Note that in between we can add ‘0’ and ‘0’ but at the last chance, we don’t want to surround with ‘0’ and ‘0’. Because we don’t want a “0110” in the solution. This is not part of the description of the problem. But based on the example given above, it doesn’t contain “00” in the answer, so that’s how we can guess we should not contain ‘0’ and ‘0’.

This problem can also be solved by using iteration. When doing iteration, it’s actually doing the same procedure as above. It’s just not using recursion.
Also we need to have the same base case [“”] or [“1″,”0″,”8”] to start with.

### Solutions:

```java
public class Solution {
    public List<String> findStrobogrammatic(int n) {
        HashMap<Character, Character> map = new HashMap<Character, Character>();
        map.put('1','1');
        map.put('0','0');
        map.put('8','8');
        map.put('6','9');
        map.put('9','6');
        return fs(map, 0, n - 1, false);
    }
    private List<String> fs(HashMap<Character, Character> map, int left, int right, boolean zeroAllow) {
        List<String> result = new LinkedList<String>();
        if (left > right) {
            result.add("");
            return result;
        }
        if (left == right) {
            result.add("1");
            result.add("0");
            result.add("8");
            return result;
        }
        List<String> inner = fs(map, left + 1, right - 1, true);
        for (String s:inner) {
            for (Character c:map.keySet()) {
                if (zeroAllow || (char)c!='0') {
                    result.add(c + s + map.get(c));
                }
            }
        }
        return result;
    }
}
```
```java
public class Solution {
    public List<String> findStrobogrammatic(int n) {
        HashMap<Character, Character> map = new HashMap<Character, Character>();
        map.put('1','1');
        map.put('0','0');
        map.put('8','8');
        map.put('6','9');
        map.put('9','6');
        List<String> result = new LinkedList<String>();
        if (n <= 0) {
            return result;
        }
 
        result.add("1");
        result.add("0");
        result.add("8");
        if (n == 1) {
            return result;
        }
        if (n % 2 != 0) {
            n --;
        }
        else {
            result.clear();
            result.add("");
        }
        while (n > 1) {
            List<String> newresult = new LinkedList<String>();
            for (String s:result) {
                for (Character c:map.keySet()) {
                    if (n != 2 || c != '0') {
                        newresult.add(c + s + map.get(c));
                    }
                }
            }
            result = newresult;
            n = n - 2;
        }     
        return result;
    }
 
}
```
