# 460. LFU Cache

### Problem:
Design and implement a data structure for Least Frequently Used (LFU) cache. It should support the following operations: get and put.

get(key) - Get the value (will always be positive) of the key if the key exists in the cache, otherwise return -1.
put(key, value) - Set or insert the value if the key is not already present. When the cache reaches its capacity, it should invalidate the least frequently used item before inserting a new item. For the purpose of this problem, when there is a tie (i.e., two or more keys that have the same frequency), the least recently used key would be evicted.

Follow up:
Could you do both operations in O(1) time complexity?

Example:
```
LFUCache cache = new LFUCache( 2 /* capacity */ );

cache.put(1, 1);
cache.put(2, 2);
cache.get(1);       // returns 1
cache.put(3, 3);    // evicts key 2
cache.get(2);       // returns -1 (not found)
cache.get(3);       // returns 3.
cache.put(4, 4);    // evicts key 1.
cache.get(1);       // returns -1 (not found)
cache.get(3);       // returns 3
cache.get(4);       // returns 4
```

### Solutions:

```java
public class LFUCache {
    private class Node {
        public Node pre;
        public Node next;
        public int key;
        public int val;
        public int freq;
        public Node (int key, int val) {
            this.key = key;
            this.val = val;
            this.pre = null;
            this.next = null;
            this.freq = 0;
        }
    }
    private HashMap<Integer, Node> heads;
    private HashMap<Integer, Node> tails;
    private HashMap<Integer, Node> data;
    private PriorityQueue<Integer> freqs;
    private int capa;
    public LFUCache(int capacity) {
        this.capa = capacity;
        heads = new HashMap<Integer, Node>();
        tails = new HashMap<Integer, Node>();
        heads.put(0, new Node(-1, -1));
        tails.put(0, new Node(-1, -1));
        heads.get(0).next = tails.get(0);
        tails.get(0).pre = heads.get(0);
        data = new HashMap<Integer, Node>();
        freqs = new PriorityQueue<Integer>();
    }
    
    public int get(int key) {
        if (!data.containsKey(key) || capa == 0) {
            return -1;
        }
        Node n = data.get(key);
        increase(n);
        return n.val;
    }
    private void increase(Node n) {
        freqs.remove(n.freq);
        n.freq ++;
        freqs.add(n.freq);
        remove(n);
        if (!heads.containsKey(n.freq)) {
            heads.put(n.freq, new Node(-1, -1));
            tails.put(n.freq, new Node(-1, -1));
            heads.get(n.freq).next = tails.get(n.freq);
            tails.get(n.freq).pre = heads.get(n.freq);
        }
        // Node head = heads.get(n.freq);
        Node tail = tails.get(n.freq);
        n.pre = tail.pre;
        tail.pre = n;
        n.pre.next = n;
        n.next = tail;
    }
    private void remove(Node n) {
        Node pre = n.pre;
        Node next = n.next;
        pre.next = next;
        next.pre = pre;
    }
    public void put(int key, int value) {
        if (capa == 0) {
            return;
        }
        if (data.containsKey(key)) {
            data.get(key).val = value;
            increase(data.get(key));
            return;
        }
        if (data.size() == capa) {
            int freq = freqs.poll();
            Node n = heads.get(freq).next;
            remove(n);
            data.remove(n.key);
        }
        Node n = new Node(key, value);
        data.put(key, n);
        heads.get(0).next = n;
        n.pre = heads.get(0);
        tails.get(0).pre = n;
        n.next = tails.get(0);
        increase(n);
    }
}

/**
 * Your LFUCache object will be instantiated and called as such:
 * LFUCache obj = new LFUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
```