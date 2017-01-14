# 288 Unique Word Abbreviation

### Problem：

<pre>
An abbreviation of a word follows the form <first letter><number><last letter>. Below are some examples of word abbreviations:

a) it                      --> it    (no abbreviation)

     1
b) d|o|g                   --> d1g

              1    1  1
     1---5----0----5--8
c) i|nternationalizatio|n  --> i18n

              1
     1---5----0
d) l|ocalizatio|n          --> l10n
Assume you have a dictionary and given a word, find whether its abbreviation is unique in the dictionary. A word's abbreviation is unique if no other word from the dictionary has the same abbreviation.

Example: 
Given dictionary = [ "deer", "door", "cake", "card" ]

isUnique("dear") -> 
false

isUnique("cart") -> 
true

isUnique("cane") -> 
false

isUnique("make") -> 
true
</pre>

### Solutions:

```java
public class ValidWordAbbr {
    HashMap<String, Integer> app = new HashMap<String, Integer>();
    HashSet<String> cand = new HashSet();
    public ValidWordAbbr(String[] dictionary) {
        for (int i = 0; i < dictionary.length; i ++) {
            if (cand.contains(dictionary[i])) {
                continue;
            }
            String s = encode(dictionary[i]);
            if (!app.containsKey(s)) {
                app.put(s, 1);
            }
            else {
                app.put(s, app.get(s) + 1);
            }
            cand.add(dictionary[i]);
        }
    }
    private String encode(String s) {
        if (s.length() <= 2) {
            return s;
        }
        String result = s.charAt(0) + "" + (s.length() - 2) + "" + s.charAt(s.length() - 1);
        return result;
    }

    public boolean isUnique(String word) {
        String s = encode(word);
        if (app.containsKey(s)) {
            if (!cand.contains(word)) {
                return false;
            }
            return app.get(s) == 1;
        }
        else {
            if (!cand.contains(word)) {
                return true;
            }
            return false;
        }
    }
}


// Your ValidWordAbbr object will be instantiated and called as such:
// ValidWordAbbr vwa = new ValidWordAbbr(dictionary);
// vwa.isUnique("Word");
// vwa.isUnique("anotherWord");
```

```java
public class ValidWordAbbr {
    HashMap<String, String> app = new HashMap<String, String>();
    public ValidWordAbbr(String[] dictionary) {
        for (int i = 0; i < dictionary.length; i ++) {
            String s = encode(dictionary[i]);
            if (app.containsKey(s) && !app.get(s).equals(dictionary[i])) {
                app.put(s, "");
            }
            else {
                app.put(s, dictionary[i]);
            }
        }
    }
    private String encode(String s) {
        if (s.length() <= 2) {
            return s;
        }
        String result = s.charAt(0) + "" + (s.length() - 2) + "" + s.charAt(s.length() - 1);
        return result;
    }

    public boolean isUnique(String word) {
        String s = encode(word);
        if (app.containsKey(s)) {
            return app.get(s).equals(word);
        }
        return true;
    }
}


// Your ValidWordAbbr object will be instantiated and called as such:
// ValidWordAbbr vwa = new ValidWordAbbr(dictionary);
// vwa.isUnique("Word");
// vwa.isUnique("anotherWord");
```