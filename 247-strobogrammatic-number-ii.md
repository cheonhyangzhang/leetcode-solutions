# 247 Strobogrammatic Number II

### Problem:

A strobogrammatic number is a number that looks the same when rotated 180 degrees (looked at upside down).

Find all strobogrammatic numbers that are of length = n.

For example,
Given n = 2, return ["11","69","88","96"].

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

```java
class Solution {
    public List<String> findStrobogrammatic(int n) {
        List<String> res = new LinkedList<String>();
        if (n == 0) {
            return res;
        }
        return fs(n, n);
    }
    private List<String> fs(int n, int target) {
        List<String> res = new LinkedList<String>();
        if (n == 0) {
            res.add("");
            return res;
        }
        if (n == 1) {
            res.add("0");
            res.add("1");
            res.add("8");
            return res;
        }
        List<String> tmp = fs(n - 2, target);
        for (String str:tmp) {
            res.add("1" + str + "1");
            res.add("8" + str + "8");
            res.add("6" + str + "9");
            res.add("9" + str + "6");
            if (n != target) {
                res.add("0" + str + "0");
            }
        }
        return res;
    }
}
```