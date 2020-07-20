Remove all elements from a linked list of integers that have value val.

Example:
```
Input:  1->2->6->3->4->5->6, val = 6
Output: 1->2->3->4->5
```

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode removeElements(ListNode head, int val) {
        if(head==null || (head.next==null  && head.val==val)) return null;
        while(head!=null && head.val==val) head=head.next;
        ListNode curr=head;
        while(curr!=null){
            while(curr.next!=null && curr.next.val!=val){
                curr=curr.next;
            }
            if(curr.next!=null && curr.next.val==val){
                curr.next=curr.next.next;
            } else {
                curr=curr.next;
            }
        }
        return head;
    }
}
```
