# 716 Max Stack

### Problem
Design a max stack that supports push, pop, top, peekMax and popMax.

1. push(x) -- Push element x onto stack.
2. pop() -- Remove the element on top of the stack and return it.
3. top() -- Get the element on the top.
4. peekMax() -- Retrieve the maximum element in the stack.
5. popMax() -- Retrieve the maximum element in the stack, and remove it. If you find more than one maximum elements, only remove the top-most one.

Example 1:
```
MaxStack stack = new MaxStack();
stack.push(5); 
stack.push(1);
stack.push(5);
stack.top(); -> 5
stack.popMax(); -> 5
stack.top(); -> 1
stack.peekMax(); -> 5
stack.pop(); -> 1
stack.top(); -> 5
```
Note:
-1e7 <= x <= 1e7
Number of operations won't exceed 10000.
The last four operations won't be called when stack is empty.

### Solutions:

```java
class MaxStack {
    PriorityQueue<Integer> q = new PriorityQueue<Integer>(10, Collections.reverseOrder());
    HashMap<Integer, LinkedList<Node>> index = new HashMap<Integer, LinkedList<Node>>();
    Node head = new Node(-1);
    Node tail = new Node(-1);
    class Node {
        public int val;
        public Node pre;
        public Node next;
        public Node(int val) {
            this.val = val;
        }
    }
    /** initialize your data structure here. */
    public MaxStack() {
        head.next = tail;
        tail.pre = head;
    }
    
    public void push(int x) {
        Node n = new Node(x);
        n.pre = tail.pre;
        n.next = tail;
        tail.pre.next = n;
        tail.pre = n;
        q.add(x);
        if (!index.containsKey(x)) {
            index.put(x, new LinkedList<Node>());
        }
        index.get(x).add(n);
    }
    
    public int pop() {
        int res = tail.pre.val;
        tail.pre.pre.next = tail;
        tail.pre = tail.pre.pre;
        q.remove(res);
        index.get(res).pollLast();
        return res;
    }
    
    public int top() {
        return tail.pre.val;
    }
    
    public int peekMax() {
        return q.peek();
    }
    
    public int popMax() {
        int res = q.poll();
        Node toRemove = index.get(res).pollLast();
        toRemove.pre.next = toRemove.next;
        toRemove.next.pre = toRemove.pre;
        return res;
    }
}

/**
 * Your MaxStack object will be instantiated and called as such:
 * MaxStack obj = new MaxStack();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.top();
 * int param_4 = obj.peekMax();
 * int param_5 = obj.popMax();
 */
```