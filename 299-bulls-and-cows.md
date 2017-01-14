# 299. Bulls and Cows

### Problem:

You are playing the following Bulls and Cows game with your friend: You write down a number and ask your friend to guess what the number is. Each time your friend makes a guess, you provide a hint that indicates how many digits in said guess match your secret number exactly in both digit and position (called "bulls") and how many digits match the secret number but locate in the wrong position (called "cows"). Your friend will use successive guesses and hints to eventually derive the secret number.

For example:

Secret number:  "1807"
Friend's guess: "7810"
Hint: 1 bull and 3 cows. (The bull is 8, the cows are 0, 1 and 7.)
Write a function to return a hint according to the secret number and friend's guess, use A to indicate the bulls and B to indicate the cows. In the above example, your function should return "1A3B".

Please note that both secret number and friend's guess may contain duplicate digits, for example:

Secret number:  "1123"
Friend's guess: "0111"
In this case, the 1st 1 in friend's guess is a bull, the 2nd or 3rd 1 is a cow, and your function should return "1A1B".
You may assume that the secret number and your friend's guess only contain digits, and their lengths are always equal.

### Solutions:

```java
public class Solution {
    public String getHint(String secret, String guess) {
        int bulls = 0;
        int cows = 0;
        HashMap<Character, Integer> sec = new HashMap<Character, Integer>();
        HashMap<Character, Integer> gue = new HashMap<Character, Integer>();
        for (int i = 0; i < secret.length(); i ++) {
            if (secret.charAt(i) == guess.charAt(i)) {
                bulls ++;
            }
            else {
                char a = secret.charAt(i);
                char b = guess.charAt(i);
                if (!sec.containsKey(a)) {
                    sec.put(a, 1);
                }
                else {
                    sec.put(a, sec.get(a) + 1);
                }
                if (!gue.containsKey(b)) {
                    gue.put(b, 1);
                }
                else {
                    gue.put(b, gue.get(b) + 1);
                }
            }
        }
        for (Character c:gue.keySet()) {
            if (sec.containsKey(c)) {
                cows += Math.min(sec.get(c), gue.get(c));
            }
        }
        return bulls + "A" + cows + "B";
    }
}
```

```java
public class Solution {
    public String getHint(String secret, String guess) {
        int bulls = 0;
        int cows = 0;
        int[] sec = new int[10];
        int[] gue = new int[10];
        for (int i = 0; i < secret.length(); i ++) {
            if (secret.charAt(i) == guess.charAt(i)) {
                bulls ++;
            }
            else {
                sec[secret.charAt(i) - '0'] ++;
                gue[guess.charAt(i) - '0'] ++;
            }
        }
        for (int i = 0; i < sec.length; i ++) {
            cows += Math.min(sec[i], gue[i]);
        }
        return bulls + "A" + cows + "B";
    }
}
```