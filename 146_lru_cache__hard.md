# 146 LRU Cache – Hard


### Problem:


Design and implement a data structure for Least Recently Used (LRU) cache. It should support the following operations: get and set.

get(key) – Get the value (will always be positive) of the key if the key exists in the cache, otherwise return -1.
set(key, value) – Set or insert the value if the key is not already present. When the cache reached its capacity, it should invalidate the least recently used item before inserting a new item.

### Thoughts:


By using a HashMap, it’s easy to implement normal set and get of the cache.
The most tricky part is that how to find the least used element.
The idea here is to use a list to keep the elements so that the least used element is in the right.
Whenever we get or set with a key, we move the element to the most right of the list so that it will be removed from the list last.

In order to make codes look cleaner, we need to have a head and tail which is dummy node.


### Solutions:


```java
public class LRUCache {
    private class Node{
        Node prev;
        Node next;
        int key;
        int value;
 
        public Node(int key, int value) {
            this.key = key;
            this.value = value;
            this.prev = null;
            this.next = null;
        }
    }
 
    private int capacity;
    private HashMap<Integer, Node> hs = new HashMap<Integer, Node>();
    private Node head = new Node(-1, -1);
    private Node tail = new Node(-1, -1);
 
    public LRUCache(int capacity) {
        this.capacity = capacity;
        tail.prev = head;
        head.next = tail;
    }
 
    public int get(int key) {
        if( !hs.containsKey(key)) {
            return -1;
        }
        Node current = hs.get(key);
        current.prev.next = current.next;
        current.next.prev = current.prev;
        moveToTail(current);
 
        return hs.get(key).value;
    }
 
    public void set(int key, int value) {
        if( get(key) != -1) {
            hs.get(key).value = value;
            return;
        }
 
        if (hs.size() == capacity) {
            hs.remove(head.next.key);
            head.next = head.next.next;
            head.next.prev = head;
        }
 
        Node insert = new Node(key, value);
        hs.put(key, insert);
        moveToTail(insert);
    }
 
    private void moveToTail(Node current) {
        current.prev = tail.prev;
        tail.prev = current;
        current.prev.next = current;
        current.next = tail;
    }
}
```