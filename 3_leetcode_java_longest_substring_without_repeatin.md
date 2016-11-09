# 3 LeetCode Java: Longest Substring Without Repeating Characters


### Problem:


Given a string, find the length of the longest substring without repeating characters. For example, the longest substring without repeating letters for “abcabcbb” is “abc”, which the length is 3. For “bbbbb” the longest substring is “b”, with the length of 1.


### Thoughts:


Keep a set of flags to indicate what character has appeared.
We could use a HashSet

There could be a optimization about the HashSet. Instead to use a set of character, use a boolean array of 256 elements saves more space when n becomes larger (n is the number of elements in the given array). Because a Character takes 16-bit and a boolean only takes 1 bit. So no matter what n is, using boolean array only takes 256 bit at most.


### Solutions:


This is the optimized version using boolean array.

```java
public class Solution {
    public int lengthOfLongestSubstring(String s) {
        boolean[] flag = new boolean[256];
 
        int result = 0;
        int start = 0;
        char[] arr = s.toCharArray();
        for (int i = 0; i < arr.length; i++) {
            char current = arr[i];
            if (flag[current]) {
                result = Math.max(result, i - start);
                for (int k = start; k < i; k++) {
                    if (arr[k] == current) {
                        start = k + 1;
                        break;
                    }
                    flag[arr[k]] = false;
                }
            } else {
                flag[current] = true;
            }
        }
        result = Math.max(arr.length - start, result);
 
        return result;
    }
}
```
Updated: 10/13/2016

The code above, because of cleaning the flags by

`for (int k = start; k < i; k++) {`
The solution will have two pass of the array, which is 2n operations. The new solution below will only have one pass of the array which is more efficient in running time. But from algorithm analysis point, they are both O(n). Also note the solution below requires to use HashMap instead of HashSet in the above.
```java
public class Solution {
  public int lengthOfLongestSubstring(String s) {
    HashMap<Character, Integer> helper = new HashMap<Character, Integer>();
    int max = 0;
    int start = 0;
    for (int i = 0; i < s.length(); i ++) {
      char c = s.charAt(i);
      if (!helper.containsKey(c) || helper.get(c) < start) {
        helper.put(c, i);
        continue;
      }
      max = Math.max(max, i - start);
      start = helper.get(c) + 1;
      helper.put(c, i);
    }
    max = Math.max(max, s.length() - start);
    return max;
  }
}
```
Another version of the solution is inspired by the official article of leetcode
```java
public class Solution {
  public int lengthOfLongestSubstring(String s) {
    int max = 0;
    Map<Character, Integer> map = new HashMap<>();
    // range is [start, i]
    int start = 0;
    for (int i = 0; i < s.length(); i++) {
      if (map.containsKey(s.charAt(i))) {
        start = Math.max(map.get(s.charAt(i)) + 1, start);
      }
      max = Math.max(max, i - start + 1);
      map.put(s.charAt(i), i);
    }
    return max;
  }
}
```