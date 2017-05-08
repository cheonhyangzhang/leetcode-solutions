# 169 Majority Element – Easy

### Problem:
Given an array of size n, find the majority element. The majority element is the element that appears more than ⌊ n/2 ⌋ times.

You may assume that the array is non-empty and the majority element always exist in the array.

### Thoughts:

Use a counter for currently met element. Since the major element will eventually win no matter where it starts.

### Solutions:

```java
public class Solution {
    public int majorityElement(int[] num) {
        int candidate = num[0];
        int counter = 1;
        for (int i = 1; i < num.length; i ++){
            if (counter == 0){
                candidate = num[i];
                counter = 1;
            }
            else{
                if (num[i] == candidate)
                    counter ++;
                else
                    counter --;
            }
        }//for i
        return candidate;
    }
}
```