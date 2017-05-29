# 248 Strobogrammatic Number III


### Problem:

A strobogrammatic number is a number that looks the same when rotated 180 degrees (looked at upside down).

Write a function to count the total strobogrammatic numbers that exist in the range of low <= num <= high.

For example,
Given low = "50", high = "100", return 3. Because 69, 88, and 96 are three strobogrammatic numbers.

Note:
Because the range might be a large number, the low and high numbers are represented as string.

### Thoughts:

This is an extension of version II. See 247 LeetCode Java: Strobogrammatic Number II – Medium.
With the solution we have in version II, we can easily get all the strobogrammatic string that has length of n.
We just need to only count the number that meets criteria low <= num <= high.
The easiest way is to get all the strobogrammatic strings, that has length of low.length() to high.length(). And iterate over every of them and check if they meets the criteria above.

The solution below is adding some more if to avoid unnecessary iteration. It doesn't affect the running time in O. Because in order to generate a list of n, it needs O(n), and if we add one more iteration on the list the time stays in O(n).

### Solutions:

```java
public class Solution {
    public int strobogrammaticInRange(String low, String high) {
        if (low.length() > high.length() || (low.length() == high.length() && low.compareTo(high) == 1)) {
            return 0;
        }
        int n1 = low.length();
        int n2 = high.length();
        int count = 0;
        if (n1 == n2) {
            List<String> tmp = findStrobogrammatic(n1);
            for (String s:tmp) {
                if (s.compareTo(low) >= 0 && s.compareTo(high) <= 0) {
                    count ++;
                }
            }
            return count;
        }
        List<String> tmp = findStrobogrammatic(n1);
        for (String s:tmp) {
            if (s.compareTo(low) >= 0) {
                count ++;
            }
        }
        tmp = findStrobogrammatic(n2);
        for (String s:tmp) {
            if (s.compareTo(high) <= 0) {
                count ++;
            }
        }
        for (int i = n1 + 1; i < n2; i ++) {
            int size = findStrobogrammatic(i).size();
            count += size;
        }
        return count;
 
    }
    //from solution of version II problem
    private List<String> findStrobogrammatic(int n) {
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
public class Solution {
    private int res = 0;
    public int strobogrammaticInRange(String low, String high) {
        for (int i = low.length(); i <= high.length(); ++i) {
            find(low, high, "", i);
            find(low, high, "0", i);
            find(low, high, "1", i);
            find(low, high, "8", i);
        }
        return res;
    }
    void find(String low, String high, String path, int len) {
        if (path.length() >= len) {
            if (path.length() != len || (len != 1 && path.charAt(0) == '0')) return;
            if ((len == low.length() && path.compareTo(low) < 0) || (len == high.length() && path.compareTo(high) > 0)) {
                return;
            }
            ++res;
        }
        find(low, high, "0" + path + "0", len);
        find(low, high, "1" + path + "1", len);
        find(low, high, "6" + path + "9", len);
        find(low, high, "8" + path + "8", len);
        find(low, high, "9" + path + "6", len);
    }
}
```