Merge two sorted linked lists and return it as a new sorted list. The new list should be made by splicing together the nodes of the first two lists.
```
Example:
Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4
```
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode tummy=new ListNode(0);
        ListNode l3=tummy;
        while(l1!=null && l2!=null){
            if(l1.val<l2.val){
                ListNode newNode=new ListNode(l1.val);
                l1=l1.next;
                l3.next=newNode;
                l3=newNode;
            }
            else{
                ListNode newNode=new ListNode(l2.val);
                l2=l2.next;
                l3.next=newNode;
                l3=newNode;
            }
        }
        l3.next=l1==null?l2:l1;
        return tummy.next;
    }
}
```
