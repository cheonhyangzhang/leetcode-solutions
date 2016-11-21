# 43  Multiply Strings – Medium


### Problem:



Given two numbers represented as strings, return multiplication of the numbers as a string.

Note: The numbers can be arbitrarily large and are non-negative.


### Thoughts:


For String number calculation problem, it’s always a good practice to reverse the string first, so that you could start calculation from left to right.

The most straight forward way to solve Multiply String problem it so mimic human calculation, iterate over one string, use the current digit to multiply the other string. Adds each temp result.

If give strings have length m and n, this approach will end up with O(mn).

But the approach above has one more thing that is you have to implement String addition as well.

There is a work around for this, from the time complicity, it’s not a big improvement, but is makes code easier. The key ideas is to calculate the multiplied result for each digit in the result. Then formalized the array of digits of the result.


### Solutions:



```java
public class Solution {
    public String multiply(String num1, String num2) {
        String n1 = new StringBuilder(num1).reverse().toString();
        String n2 = new StringBuilder(num2).reverse().toString();
        int[] d = new int[n1.length()+n2.length()];
        for(int i=0; i < n1.length(); i++){
            for(int j=0; j < n2.length(); j++){
                d[i+j] += (n1.charAt(i)-'0') * (n2.charAt(j)-'0');
            }
        }
 
        String result = "";
        for(int i=0; i < d.length; i++){
            int digit = d[i]%10;
            int carry = d[i]/10;
            if(i+1 < d.length){ 
                d[i+1] += carry; 
            }  
            result = (digit + "") + result;
        } 
        int index = 0;        
        while(index < result.length() - 1 && result.charAt(index)=='0'){
            index ++;
        }
        return result.substring(index);
 
    }
}
```