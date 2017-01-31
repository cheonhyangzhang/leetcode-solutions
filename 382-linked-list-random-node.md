# 382. Linked List Random Node

### Problem:

Given a singly linked list, return a random node's value from the linked list. Each node must have the same probability of being chosen.

Follow up:
What if the linked list is extremely large and its length is unknown to you? Could you solve this efficiently without using extra space?

Example:

```
// Init a singly linked list [1,2,3].
ListNode head = new ListNode(1);
head.next = new ListNode(2);
head.next.next = new ListNode(3);
Solution solution = new Solution(head);

// getRandom() should return either 1, 2, or 3 randomly. Each element should have equal probability of returning.
solution.getRandom();
```

### Solutions:

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
public class Solution {
    private HashMap<Integer, Integer> indexToNum;
    private int size = 0;
    private Random r;
    /** @param head The linked list's head.
        Note that the head is guaranteed to be not null, so it contains at least one node. */
    public Solution(ListNode head) {
        indexToNum = new HashMap<Integer, Integer>();
        while (head != null) {
            indexToNum.put(size++, head.val);
            head = head.next;
        }
        r = new Random();
    }
    
    /** Returns a random node's value. */
    public int getRandom() {
        if (size > 0) {
            int index = r.nextInt(size);
            int val = indexToNum.get(index);
            return val;
        }
        return -1;
    }
}

/**
 * Your Solution object will be instantiated and called as such:
 * Solution obj = new Solution(head);
 * int param_1 = obj.getRandom();
 */
```

