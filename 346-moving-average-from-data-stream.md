# 346. Moving Average from Data Stream

### Problem:

<pre>
Given a stream of integers and a window size, calculate the moving average of all integers in the sliding window.

For example,
MovingAverage m = new MovingAverage(3);
m.next(1) = 1
m.next(10) = (1 + 10) / 2
m.next(3) = (1 + 10 + 3) / 3
m.next(5) = (10 + 3 + 5) / 3
</pre>

### Solutions:

```java
public class MovingAverage {

    private int size;
    private Queue<Integer> data;
    private long sum;
    /** Initialize your data structure here. */
    public MovingAverage(int size) {
        this.size = size;
        data = new LinkedList<Integer>();
        sum = 0;
    }
    
    public double next(int val) {
        data.add(val);
        sum = sum + val;
        if (data.size() > size) {
            sum = sum - data.poll();
        }
        return (double)sum / (double) data.size();
    }
}

/**
 * Your MovingAverage object will be instantiated and called as such:
 * MovingAverage obj = new MovingAverage(size);
 * double param_1 = obj.next(val);
 */
```

