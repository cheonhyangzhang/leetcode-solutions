# 294 Flip Game II

### Problem:

You are playing the following Flip Game with your friend: Given a string that contains only these two characters: + and -, you and your friend take turns to flip two consecutive "++" into "--". The game ends when a person can no longer make a move and therefore the other person will be the winner.

Write a function to determine if the starting player can guarantee a win.

For example, given s = "++++", return true. The starting player can guarantee a win by flipping the middle "++" to become "+--+".

Follow up:
Derive your algorithm's runtime complexity.

### Solutions:

```java
public class Solution {
    HashMap<String, Boolean> win = new HashMap<String, Boolean>();
    public boolean canWin(String s) {
        if (win.containsKey(s)) {
            return win.get(s);
        }
        StringBuilder sb = new StringBuilder(s);
        for (int i = 0; i < s.length() - 1; i ++) {
            if (s.charAt(i) == '+' && s.charAt(i + 1) == '+') {
                sb.setCharAt(i, '-');
                sb.setCharAt(i + 1, '-');
                if (!canWin(sb.toString())) {
                    win.put(s, true);
                    return true;
                }
                sb.setCharAt(i, '+');
                sb.setCharAt(i + 1, '+');
            }
            
        }
        win.put(s, false);
        return false;
    }
}
```