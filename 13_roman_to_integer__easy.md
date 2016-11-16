# 13 Roman to Integer – Easy


### Problem:



Given a roman numeral, convert it to an integer.

Input is guaranteed to be within the range from 1 to 3999.


### Thoughts:



The most straightforward way is to calculate by imitating human behavior.

Give a roman, find the largest digit, then subtract the left part and add the right part. Do this recursively and we could get our number in the end.

This is going to be O(nlgn), where is the number of digits in Roman representation.

There is a better solution with only O(n) running time. Key idea is always add a corresponding integer number, and compare current digit if it’s larger than previous, if so, subtract double of the previous number. This is because we need to subtract previous number but we already added it to the result, so we need to double it.


### Solutions:

```java
public class Solution {
    public int romanToInt(String s) {
        HashMap<Character, Integer> helper = new HashMap<Character, Integer>();
        initHelper(helper);
        int result = 0;
        for (int i = 0; i < s.length(); i ++){
            if ( i > 0 && helper.get(s.charAt(i)) > helper.get(s.charAt(i-1))) {
                result = result - 2 * helper.get(s.charAt(i-1));
            }
            result = result + helper.get(s.charAt(i));
        }
        return result;
    }
    private void initHelper(HashMap<Character, Integer> helper) {
        helper.put('M', 1000);
        helper.put('D', 500);
        helper.put('C', 100);
        helper.put('L', 50);
        helper.put('X', 10);
        helper.put('V', 5);
        helper.put('I', 1);
         
    }
}
```
