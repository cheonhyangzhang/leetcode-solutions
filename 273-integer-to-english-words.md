# 273 Integer to English Words

### Problem

Convert a non-negative integer to its english words representation. Given input is guaranteed to be less than 231 - 1.

For example,
```
123 -> "One Hundred Twenty Three"
12345 -> "Twelve Thousand Three Hundred Forty Five"
1234567 -> "One Million Two Hundred Thirty Four Thousand Five Hundred Sixty Seven"
```

### Solutions

```java
class Solution {
    public String numberToWords(int num) {
        if (num == 0) {
            return "Zero";
        }
        ArrayList<String> unit = new ArrayList<String>();
        HashMap<Integer, String> singles = new HashMap<Integer, String>();
        HashMap<Integer, String> doubles = new HashMap<Integer, String>();
        init(unit, singles, doubles);
        String res = "";
        int index = 0;
        while (num != 0) {
            int tmp = num % 1000;
            if (tmp != 0) {
                String part = "";
                int hund = tmp / 100;
                if (hund != 0) {
                    part = part + singles.get(hund) + " Hundred";
                }
                tmp = tmp % 100;
                if (tmp >= 10 && tmp <= 19) {
                    part = part + " " + doubles.get(tmp);
                }
                else {
                    int tens = tmp / 10;
                    if (tens != 0) {
                        part = part + " " + doubles.get(tens);
                    }
                    int ones = tmp % 10;
                    if (ones != 0) {
                        part = part + " " + singles.get(ones);
                    }
                }
                part = part + " " + unit.get(index);
                part = part.trim() + " ";
                res = part + res;
            }
            index ++;
            num = num / 1000;
        }
        return res.trim();
    }
    private void init(ArrayList<String> unit, HashMap<Integer, String> singles, HashMap<Integer, String> doubles) {
        unit.add("");
        unit.add("Thousand");
        unit.add("Million");
        unit.add("Billion");
        singles.put(1, "One");
        singles.put(2, "Two");
        singles.put(3, "Three");
        singles.put(4, "Four");
        singles.put(5, "Five");
        singles.put(6, "Six");
        singles.put(7, "Seven");
        singles.put(8, "Eight");
        singles.put(9, "Nine");
        doubles.put(10, "Ten");
        doubles.put(11, "Eleven");
        doubles.put(12, "Twelve");
        doubles.put(13, "Thirteen");
        doubles.put(14, "Fourteen");
        doubles.put(15, "Fifteen");
        doubles.put(16, "Sixteen");
        doubles.put(17, "Seventeen");
        doubles.put(18, "Eighteen");
        doubles.put(19, "Nineteen");
        doubles.put(2, "Twenty");
        doubles.put(3, "Thirty");
        doubles.put(4, "Forty");
        doubles.put(5, "Fifty");
        doubles.put(6, "Sixty");
        doubles.put(7, "Seventy");
        doubles.put(8, "Eighty");
        doubles.put(9, "Ninety");
    }
}
```

