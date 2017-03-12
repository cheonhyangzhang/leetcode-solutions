# 295 Find Median from Data Stream

### Problem:

Median is the middle value in an ordered integer list. If the size of the list is even, there is no middle value. So the median is the mean of the two middle value.

Examples: 
[2,3,4] , the median is 3

[2,3], the median is (2 + 3) / 2 = 2.5

Design a data structure that supports the following two operations:

void addNum(int num) - Add a integer number from the data stream to the data structure.
double findMedian() - Return the median of all elements so far.
For example:
```
addNum(1)
addNum(2)
findMedian() -> 1.5
addNum(3) 
findMedian() -> 2
```

### Solutions:

```java
public class MedianFinder {
    PriorityQueue<Integer> left;
    PriorityQueue<Integer> right;
    /** initialize your data structure here. */
    public MedianFinder() {
        left = new PriorityQueue<Integer>(Collections.reverseOrder());
        right = new PriorityQueue<Integer>();
    }
    
    public void addNum(int num) {
        double median = findMedian();
        if (left.size() == right.size()) {
            if (num < median) {
                left.add(num);
            }
            else {
                right.add(num);
            }
        }
        else if (left.size() > right.size()) {
            if (num > median) {
                right.add(num);
            }
            else {
                right.add(left.poll());
                left.add(num);
            }
        }
        else {
            if (num < median) {
                left.add(num);
            }
            else {
                left.add(right.poll());
                right.add(num);
            }
        }
    }
    
    public double findMedian() {
        if (left.isEmpty() && right.isEmpty()) {
            return 0;
        }
        if (left.size() == right.size()) {
            return (double)(left.peek() + right.peek()) / 2;
        }
        if (left.size() > right.size()) {
            return left.peek();
        }
        else {
            return right.peek();
        }
    }
}

/**
 * Your MedianFinder object will be instantiated and called as such:
 * MedianFinder obj = new MedianFinder();
 * obj.addNum(num);
 * double param_2 = obj.findMedian();
 */
```