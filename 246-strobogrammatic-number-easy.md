# 246 Strobogrammatic Number – Easy

### Problem:
A strobogrammatic number is a number that looks the same when rotated 180 degrees (looked at upside down).

Write a function to determine if a number is strobogrammatic. The number is represented as a string.

For example, the numbers “69”, “88”, and “818” are all strobogrammatic.

### Thoughts:
This is actually almost the same problem as 125 LeetCode Java: Valid Palindrome – Easy. But now the condition is not to check if two char in the front and back are the same but to check if they meet the requirement on mapping.

1->1, 8->8, 0->0, 6->9 and 9->6 is the mapping.

### Solutions:

```java
public class Solution {
    public boolean isStrobogrammatic(String num) {
        HashMap<Character, Character> map = new HashMap<Character, Character>();
        map.put('1','1');
        map.put('0','0');
        map.put('8','8');
        map.put('6','9');
        map.put('9','6');
        int left = 0, right = num.length() - 1;
        while (left <= right) {
            if (!map.containsKey(num.charAt(left)) || !map.get(num.charAt(left)).equals(num.charAt(right))) {
                return false;
            }
            left ++;
            right --;
        }
        return true;
    }
}
```