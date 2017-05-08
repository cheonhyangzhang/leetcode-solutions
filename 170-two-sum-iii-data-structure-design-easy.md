# 170 Two Sum III – Data structure design – Easy

### Problem:
Design and implement a TwoSum class. It should support the following operations: add and find.

add – Add the number to an internal data structure.
find – Find if there exists any pair of numbers which sum is equal to the value.

For example,
add(1); add(3); add(5);
find(4) -> true
find(7) -> false

### Thoughts:
There could be many ways to design the data structure.
With considering about performance, I choose using a HashMap, which will end up with O(1) for adding and O(n) for finding.

### Solutions:

```java
public class TwoSum {
    private HashMap<Integer, Integer> count = new HashMap<Integer, Integer>();
    // Add the number to an internal data structure.
    public void add(int number) {
       // data.add(number);
        if (count.containsKey(number)) {
            count.put(number, count.get(number) + 1);
        }
        else {
            count.put(number, 1);
        }
    }
 
    // Find if there exists any pair of numbers which sum is equal to the value.
    public boolean find(int value) {
        for (Integer key:count.keySet()) {
            if (2*key == value && count.get(key) >=2) {
                return true;
            }
            if (2*key != value && count.containsKey(value - key)) {
                return true;
            }
        }
        return false;
    }
}
 
 
// Your TwoSum object will be instantiated and called as such:
// TwoSum twoSum = new TwoSum();
// twoSum.add(number);
// twoSum.find(value);
```