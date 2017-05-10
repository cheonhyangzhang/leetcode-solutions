# 179 Largest Number – Medium

### Problem:
Given a list of non negative integers, arrange them such that they form the largest number.

For example, given [3, 30, 34, 5, 9], the largest formed number is 9534330.

Note: The result may be very large, so you need to return a string instead of an integer.

### Thoughts:
The trick is to implement a custom comparator then leverage Arrays.sort method.
Also, note that if implement Comparator, you cannot use Arrays.sort(int[[], CustomComparator) because int cannot be automatically casted into Integer object in this case.

### Solutions:

```java
public class Solution {
    public String largestNumber(int[] nums) {
        String[] snums = new String[nums.length];
        for (int i = 0; i < nums.length; i ++){
            snums[i] = "" + nums[i];
        } 
        Arrays.sort(snums, new Comparator<String>(){
            public int compare(String a, String b){
                String atob = a + b;
                String btoa = b + a;
                return btoa.compareTo(atob);
            }
        });
        String result = "";
        for (int i = 0; i < snums.length; i ++){ 
            result +=snums[i]; 
        } //remove front zeroes 
        while (result.length() > 1){
            if (result.charAt(0) == '0')
                result = result.substring(1);
            else
                break;
        }
        return result;
    }//largestNumber
}
```

```java
public class Solution {
    class StrComparator implements Comparator<String> {
        @Override
        public int compare(String s1, String s2) {
            String s1s2 = s1 + "" + s2;
            String s2s1 = s2 + "" + s1;
            return s1s2.compareTo(s2s1);
        }
    }
    public String largestNumber(int[] nums) {
        String[] strs = new String[nums.length];
        for (int i = 0; i < nums.length; i ++) {
            strs[i] = nums[i] + "";
        }
        Arrays.sort(strs, new StrComparator());
        String result = "";
        for (int i = 0; i < strs.length; i ++) {
            result = strs[i] + result;
        }
        if (result.charAt(0) == '0') {
            return "0";
        }
        return result;
    }
}

```