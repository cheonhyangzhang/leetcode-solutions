# 432. All O`one Data Structure

### Problem
Implement a data structure supporting the following operations:

Inc(Key) - Inserts a new key with value 1. Or increments an existing key by 1. Key is guaranteed to be a non-empty string.
Dec(Key) - If Key's value is 1, remove it from the data structure. Otherwise decrements an existing key by 1. If the key does not exist, this function does nothing. Key is guaranteed to be a non-empty string.
GetMaxKey() - Returns one of the keys with maximal value. If no element exists, return an empty string "".
GetMinKey() - Returns one of the keys with minimal value. If no element exists, return an empty string "".
Challenge: Perform all these in O(1) time complexity.

### Solutions
```java
class AllOne {
    class Node {
        public Node pre;
        public Node next;
        public String key;
        public int val;
        public Node(String key, int val) {
            pre = null;
            next = null;
            this.key = key;
            this.val = val;
        }
    }
    class Freq {
        public int val;
        public Freq next;
        public Freq pre;
        public Freq(int val) {
            this.val = val;
        }
    }
    private Freq freqHead;
    private Freq freqTail;
    private HashMap<Integer, Node> heads = new HashMap<>();
    private HashMap<Integer, Freq> freqs = new HashMap<>();
    private HashMap<String, Node> data = new HashMap<>();
    /** Initialize your data structure here. */
    public AllOne() {
        freqHead = new Freq(-1);
        freqTail = new Freq(-1);
        freqHead.next = freqTail;
        freqTail.pre = freqHead;
    }
    
    /** Inserts a new key <Key> with value 1. Or increments an existing key by 1. */
    public void inc(String key) {
        if (!data.containsKey(key)) {
            Node n = new Node(key, 0);
            data.put(key, n);
            initHeads(0);
            insertNode(heads.get(0), n);
            Freq f = new Freq(0);
            freqs.put(0, f);
            insertFreq(freqHead, f);
        }
        increase(data.get(key));
    }
    // init the head for a given val
    private void initHeads(int val) {
        if (!heads.containsKey(val)) {
            Node head = new Node("", -1);
            Node tail = new Node("", -1);
            head.next = tail;
            tail.pre = head;
            heads.put(val, head);
        }
    }
    // insert a Node after Node pre
    private void insertNode(Node pre, Node n) {
        n.next = pre.next;
        n.pre = pre;
        n.pre.next = n;
        n.next.pre = n;
    }
    // insert a Freq after Freq pre
    private void insertFreq(Freq pre, Freq f) {
        f.next = pre.next;
        f.pre = pre;
        f.pre.next = f;
        f.next.pre = f;
    }
    // remove a Node from the list
    private void removeNode(Node n) {
        n.pre.next = n.next;
        n.next.pre = n.pre;
    }
    // remove a freq from the list
    private void removeFreq(Freq f) {
        f.pre.next = f.next;
        f.next.pre = f.pre;
        freqs.remove(f.val);
    }
    private void increase(Node n) {
        int val = n.val;
        n.val ++;
        Freq f = freqs.get(val);
        validate(val, n, f.next, true);
    }
    // When node is updated from val to the current node val
    // Do a validate of the data structure
    private void validate(int val, Node n, Freq lookFreq, boolean next) {
        removeNode(n);
        Freq f = freqs.get(val);
        if (n.val != 0) {
            if (lookFreq.val != n.val) {
                Freq incF = new Freq(n.val);
                freqs.put(n.val, incF);
                if (next) {
                    insertFreq(f, incF);
                }
                else {
                    insertFreq(f.pre, incF);
                }
            }
            initHeads(n.val);
            insertNode(heads.get(n.val), n);
        }
        else {
            data.remove(n.key);
        }
        if (heads.get(val).next.next == null) {
            removeFreq(f);
        }
    }
    
    /** Decrements an existing key by 1. If Key's value is 1, remove it from the data structure. */
    public void dec(String key) {
        if (!data.containsKey(key)) {
            return;
        }
        Node n = data.get(key);
        int val = n.val;
        n.val --;
        Freq f = freqs.get(val);
        validate(val, n, f.pre, false);
    }
    
    /** Returns one of the keys with maximal value. */
    public String getMaxKey() {
        if (!heads.containsKey(freqTail.pre.val)) {
            return "";
        }
        return heads.get(freqTail.pre.val).next.key;
    }
    
    /** Returns one of the keys with Minimal value. */
    public String getMinKey() {
        System.out.println("getMinKey : " + freqHead.next.val);
        if (!heads.containsKey(freqHead.next.val)) {
            return "";
        }
        return heads.get(freqHead.next.val).next.key;
    }
}

/**
 * Your AllOne object will be instantiated and called as such:
 * AllOne obj = new AllOne();
 * obj.inc(key);
 * obj.dec(key);
 * String param_3 = obj.getMaxKey();
 * String param_4 = obj.getMinKey();
 */
 ```