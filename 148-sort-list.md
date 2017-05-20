# 148 Sort List

### Problem:

Sort a linked list in O(n log n) time using constant space complexity.

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
    public ListNode sortList(ListNode head) {
        if (head == null){
            return null;
        }
        int length = 0;
        ListNode node = head;
        while (node != null){
            length ++;
            node = node.next;
        }
        
        ListNode globalHead = new ListNode(-1);
        globalHead.next = head;
        ListNode result = mergeSort(globalHead, 0, length -1);
        return result;
    }
    private ListNode mergeSort(ListNode globalHead, int start, int end){
        if (start > end){
            return null;
        }
        else if (start == end){
            ListNode tmp = globalHead.next;
            globalHead.next = globalHead.next.next;
            tmp.next = null;
            return tmp;
        }
        else{
            //start > end 
            int mid = (start + end ) /2;
            ListNode left = mergeSort(globalHead, start, mid);
            ListNode right = mergeSort(globalHead, mid + 1, end);
            return merge(left, right);
        }
    }
    private ListNode merge(ListNode left, ListNode right){
        ListNode fakeHead = new ListNode(-1);
        ListNode now = fakeHead;
        while (left!=null && right !=null){
            if (left.val < right.val){
                now.next = left;
                now = now.next;
                left = left.next;
            }
            else{
                now.next = right;
                now = now.next;
                right = right.next;
            }//else
        }//while
        if (left !=null){
            now.next = left;
        }
        if (right !=null){
            now.next = right;
        }
        return fakeHead.next;
    }
    
}
```