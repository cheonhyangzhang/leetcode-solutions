# 247 Strobogrammatic Number II

### Problem:

A strobogrammatic number is a number that looks the same when rotated 180 degrees (looked at upside down).

Find all strobogrammatic numbers that are of length = n.

For example,
Given n = 2, return ["11","69","88","96"].

### Solutions:

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

```java
class Solution {
    public List<String> findStrobogrammatic(int n) {
        List<String> res = new LinkedList<String>();
        process("", n, res);
        process("0", n, res);
        process("1", n, res);
        process("8", n, res);
        return res;
    }
    private void process(String cand, int n, List<String> res) {
        if (cand.length() > n) {
            return;
        }
        if (cand.length() == n) {
            if (cand.length() != 1 && cand.charAt(0) == '0') {
                return;
            }
            res.add(cand);
        }
        process("0" + cand + "0", n, res);
        process("1" + cand + "1", n, res);
        process("8" + cand + "8", n, res);
        process("6" + cand + "9", n, res);
        process("9" + cand + "6", n, res);
    }
}
```