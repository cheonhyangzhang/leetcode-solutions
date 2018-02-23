# 402. Remove K Digits

### Problem:
Given a non-negative integer num represented as a string, remove k digits from the number so that the new number is the smallest possible.

Note:
* The length of num is less than 10002 and will be ≥ k.
* The given num does not contain any leading zero.
Example 1:
```
Input: num = "1432219", k = 3
Output: "1219"
Explanation: Remove the three digits 4, 3, and 2 to form the new number 1219 which is the smallest.
```
Example 2:
```
Input: num = "10200", k = 1
Output: "200"
Explanation: Remove the leading 1 and the number is 200. Note that the output must not contain leading zeroes.
```
Example 3:
```
Input: num = "10", k = 2
Output: "0"
Explanation: Remove all the digits from the number and it is left with nothing which is 0.
```

### Solutions:

```java
public class Solution {
    public String removeKdigits(String num, int k) {
        if (num.length() == k) {
            return "0";
        }
        StringBuilder sb = new StringBuilder(num);
        for (int j = 0; j < k; j ++) {
            int i = 0;
            while (i < sb.length() - 1 && sb.charAt(i) <= sb.charAt(i + 1)) {
                i ++;
            }
            sb.delete(i, i + 1);
        }
        int i = 0;
        while (i < sb.length() - 1 && sb.charAt(i) == '0') {
            i ++;
        }
        return sb.toString().substring(i);
    }
}
```

```java
public class Solution {
    public String removeKdigits(String num, int k) {
        if (num.length() == k) {
            return "0";
        }
        Stack<Character> stack = new Stack<Character>();
        int i = 0;
        for (int j = 0; j < k; j ++) {
            if (i >= num.length() || (!stack.isEmpty() && stack.peek() > num.charAt(i))) {
                stack.pop();
                continue;
            }
            while (i < num.length() - 1 && num.charAt(i) <= num.charAt(i + 1)) {
                stack.push(num.charAt(i));
                i ++;
            }
            i ++;
        }
        while (i < num.length()) {
            stack.push(num.charAt(i));
            i ++;
        }
        String sb = "";
        while (!stack.isEmpty()) {
            sb = stack.pop() + sb;
        }
        i = 0;
        while (i < sb.length() - 1 && sb.charAt(i) == '0') {
            i ++;
        }
        return sb.substring(i);
    }
}
```

```java
class Solution {
    public String removeKdigits(String num, int k) {
        if (num == null || num.length() == 0) {
            return "";
        }
        if (k >= num.length()) {
            return "0";
        }
        LinkedList<Character> cands = new LinkedList<>();
        for (int i = 0; i < num.length(); i ++) {
            char c = num.charAt(i);
            while (cands.size() > 0 && c < cands.peekLast() && k > 0) {
                cands.pollLast();
                k --;
            }
            cands.add(c);
        }
        while (k > 0) {
            cands.pollLast();
            k --;
        }
        //remove leading 0
        while (cands.size() > 0 && cands.peekFirst() == '0') {
            cands.pollFirst();
        }
        if (cands.size() == 0) {
            return "0";
        }
        StringBuilder sb = new StringBuilder();
        while (cands.size() > 0) {
            sb.append(cands.pollFirst());
        }
        return sb.toString();
    }
}
```