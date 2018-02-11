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
        boolean dot = false;
        boolean num = false;
        boolean exp = false;
        boolean expcmp = false;
        boolean expbf = false;
        s = s.trim();
        if (s.length() == 0){
            return false;
        }
        if (s.charAt(0) == '-'){
            s = s.substring(1);
        }
        else if (s.charAt(0) == '+'){
            s = s.substring(1);
        }
        for (int i = 0; i < s.length(); i ++){
            char c = s.charAt(i);
            if (c == '.'){
                if (dot == true || exp == true){
                    return false;
                }
                else{
                    dot = true;
                }
            }
            else if (c == 'e'){
                if (expbf == false){
                    return false;
                }
                if (exp == true){
                    return false;
                }
                else{
                    exp = true;
                    if (i + 1 < s.length() &&(s.charAt(i+1) == '-' || s.charAt(i+1) == '+')){
                        i ++;
                    }
                }
            }
            else if (c >= '0' && c <='9'){
                num = true;
                expbf = true;
                if (exp == true){
                    expcmp = true;
                }
                continue;
            }
            else{
                return false;
            }
        }
        if (exp == true && expcmp == false){
            return false;
        }
        
        if (num == false){
            return false;
        }
        return true;
    }
}
```