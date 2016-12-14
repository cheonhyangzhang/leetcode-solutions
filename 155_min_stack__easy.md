# 155  Min Stack – Easy


### Problem:



Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

push(x) — Push element x onto stack.
pop() — Removes the element on top of the stack.
top() — Get the top element.
getMin() — Retrieve the minimum element in the stack.

### Thoughts:



The trick is to use an extra stack to keep the current min value.


### Solutions:


```java
public class MinStack {
    private Stack<Integer> data;
    private Stack<Integer> mins;
    /** initialize your data structure here. */
    public MinStack() {
        data = new Stack<Integer>();
        mins = new Stack<Integer>();
        data.push(-1);
        mins.push(Integer.MAX_VALUE);
    }
    public void push(int x) {
        data.push(x);
        mins.push(Math.min(x, mins.peek()));
    }
    public void pop() {
        if (data.size() > 1) {
            data.pop();
            mins.pop();
        }   
    }
     
    public int top() {
        return data.peek();
    }
     
    public int getMin() {
        return mins.peek();
    }
}
 
/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack obj = new MinStack();
 * obj.push(x);
 * obj.pop();
 * int param_3 = obj.top();
 * int param_4 = obj.getMin();
 */
 ```