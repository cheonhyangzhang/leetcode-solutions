# 284. Peeking Iterator

### Problem:

Given an Iterator class interface with methods: next() and hasNext(), design and implement a PeekingIterator that support the peek() operation -- it essentially peek() at the element that will be returned by the next call to next().

Here is an example. Assume that the iterator is initialized to the beginning of the list: [1, 2, 3].

Call next() gets you 1, the first element in the list.

Now you call peek() and it returns 2, the next element. Calling next() after that still return 2.

You call next() the final time and it returns 3, the last element. Calling hasNext() after that should return false.

Hint:

Think of "looking ahead". You want to cache the next element.
Is one variable sufficient? Why or why not?
Test your design with call order of peek() before next() vs next() before peek().
For a clean implementation, check out Google's guava library source code.
Follow up: How would you extend your design to be generic and work with all types, not just integer?

### Solutions:

```java
// Java Iterator interface reference:
// https://docs.oracle.com/javase/8/docs/api/java/util/Iterator.html
class PeekingIterator implements Iterator<Integer> {
    Integer peek = 0;
    boolean peeked = false;
    Iterator<Integer> it;
	public PeekingIterator(Iterator<Integer> iterator) {
	    // initialize any member here.
	    it = iterator;
	    peek = 0;
	    peeked = false;
	}

    // Returns the next element in the iteration without advancing the iterator.
	public Integer peek() {
        if (peeked) {
            return peek;
        }
        peek = it.next();
        peeked = true;
        return peek;
	}

	// hasNext() and next() should behave the same as in the Iterator interface.
	// Override them if needed.
	@Override
	public Integer next() {
	    if (peeked) {
	        int tmp = peek;
	        if (it.hasNext()) {
	            peek = it.next();
	        }
	        else {
	            peeked = false;
	        }
	        return tmp;
	    }
	    return it.next();
	}

	@Override
	public boolean hasNext() {
	    return peeked || it.hasNext();
	}
}
```

```java
// Java Iterator interface reference:
// https://docs.oracle.com/javase/8/docs/api/java/util/Iterator.html
class PeekingIterator implements Iterator<Integer> {
    Integer peek = null;
    Iterator<Integer> it;
	public PeekingIterator(Iterator<Integer> iterator) {
	    // initialize any member here.
	    it = iterator;
	    peek = null;
	}

    // Returns the next element in the iteration without advancing the iterator.
	public Integer peek() {
	    if (peek == null) {
	        peek = it.next();
	    }
        return peek;
	}

	// hasNext() and next() should behave the same as in the Iterator interface.
	// Override them if needed.
	@Override
	public Integer next() {
	    if (peek != null) {
	        Integer res = peek;
	        if (it.hasNext()) {
	            peek = it.next();
	        }
	        else {
	            peek = null;
	        }
	        return res;
	    }
	    return it.next();
	}

	@Override
	public boolean hasNext() {
	    return peek != null || it.hasNext();
	}
}
```