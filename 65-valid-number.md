# 65 Valid Number

### Problem
Validate if a given string is numeric.

Some examples:
"0" => true
" 0.1 " => true
"abc" => false
"1 a" => false
"2e10" => true
Note: It is intended for the problem statement to be ambiguous. You should gather all requirements up front before implementing one.

### Solutions

```java
public class Solution {
    public boolean isNumber(String s) {
        s = s.trim();
        if (s.indexOf("e") != -1) {
            int cut = s.indexOf("e");
            return validNumber(s.substring(0, cut), true) && validNumber(s.substring(cut + 1), false);
        }
        else {
            return validNumber(s, true);
        }
    }
    private boolean validNumber(String s, boolean canBeDouble) {
        if (s.length() == 0) {
            return false;
        }
        if (s.charAt(0) == '-' || s.charAt(0) == '+') {
            s = s.substring(1);
        }
        if (s.indexOf(".") != -1) {
            if (canBeDouble == false) {
                return false;
            }
            int cut = s.indexOf(".");
            return (validInteger(s.substring(0, cut), true) && validInteger(s.substring(cut + 1), false)) || (validInteger(s.substring(0, cut), false) && validInteger(s.substring(cut + 1), true));
        }
        else {
            return validInteger(s, false);
        }
    }
    private boolean validInteger(String s, boolean canBeEmpty) {
        if (!canBeEmpty && s.length() == 0) {
            return false;
        }
        for (int i = 0; i < s.length(); i ++) {
            char c = s.charAt(i);
            if (c < '0' || c > '9') {
                return false;
            }
        }
        return true;
    }
}
```

```java
class Solution {
    public boolean isNumber(String s) {
        s = s.trim();
        int cut = s.indexOf("e");
        if (cut != -1) {
            return isRealNumber(s.substring(0, cut), true) && isRealNumber(s.substring(cut + 1), false);
        }
        else {
            return isRealNumber(s, true);
        }
    }
    
    // assume 0001 is valid
    private boolean isRealNumber(String s, boolean canBeDouble) {
        if (s.length() > 0 && (s.charAt(0) == '-' || s.charAt(0) == '+')) {
            s = s.substring(1);
        }
        int cut = s.indexOf(".");
        if ( cut != -1) {
            if (canBeDouble == false) {
                return false;
            }
            return (isPureNumber(s.substring(0, cut), true) && isPureNumber(s.substring(cut + 1), false)) || (isPureNumber(s.substring(0, cut), false) && isPureNumber(s.substring(cut + 1), true));
        }
        else {
            return isPureNumber(s, false);
        }
    }
    private boolean isPureNumber(String s, boolean canBeEmpty) {
        if (canBeEmpty == false && s.length() == 0) {
            return false;
        }
        for (int i = 0; i < s.length(); i ++) {
            char c = s.charAt(i);
            if (c < '0' || c > '9') {
                return false;
            }
        }
        return true;
    }
}
```

```java
class Solution {
    public boolean isNumber(String s) {
        s = s.trim();
        int cut = s.indexOf("e");
        if (cut != - 1) {
            return isRational(s.substring(0, cut)) && isInteger(s.substring(cut + 1), false, true);
        }
        else {
            return isRational(s);
        }
    }
    private boolean isRational(String s) {
        int cut = s.indexOf(".");
        if (cut != -1) {
            String first = s.substring(0, cut);
            String second = s.substring(cut + 1);
            return (isInteger(first, true, true) && isInteger(second, false, false)) || (isInteger(first, false, true) && isInteger(second, true, false));
        }
        else {
            return isInteger(s, false, true);
        }
    }
    private boolean isInteger(String s, boolean canBeEmpty, boolean canHaveSign) {
        if (s.length() == 0) {
            return canBeEmpty;
        }
        if (s.charAt(0) == '-' || s.charAt(0) == '+') {
            if (canHaveSign == true) {
                s = s.substring(1);
            }
            else {
                return false;
            }
        }
        if (s.length() == 0) {
            return canBeEmpty;
        }
        for (int i = 0; i < s.length(); i ++) {
            char c = s.charAt(i);
            if (c < '0' || c > '9') {
                return false;
            }
        }
        return true;
    }
}
```