# 232 Implement Queue using Stacks – Easy

### Problem:
Implement the following operations of a queue using stacks.

push(x) — Push element x to the back of queue.
pop() — Removes the element from in front of queue.
peek() — Get the front element.
empty() — Return whether the queue is empty.
Notes:
You must use only standard operations of a stack — which means only push to top, peek/pop from top, size, and is empty operations are valid.
Depending on your language, stack may not be supported natively. You may simulate a stack by using a list or deque (double-ended queue), as long as you use only standard operations of a stack.
You may assume that all operations are valid (for example, no pop or peek operations will be called on an empty queue).

### Thoughts:
This is very similar to the previous problem Implement Stack using Queues.
The solution below is making push expensive.

### Solutions:

```java
class MyQueue {
    Stack<Integer> data = new Stack<Integer>();
    // Push element x to the back of queue.
    public void push(int x) {
        Stack<Integer> reverse = new Stack<Integer>();
        while (data.size() > 0) {
            reverse.push(data.pop());
        }
        data.push(x);
        while (reverse.size() > 0) {
            data.push(reverse.pop());
        }
    }
 
    // Removes the element from in front of queue.
    public void pop() {
        data.pop();
    }
 
    // Get the front element.
    public int peek() {
        return data.peek();
    }
 
    // Return whether the queue is empty.
    public boolean empty() {
        return data.size() == 0;
    }
}
```
