Given a linked list, return the node where the cycle begins. If there is no cycle, return null.

```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode detectCycle(ListNode head) {
        if(head==null || head.next==null)return null;
        ListNode fast = head.next.next;
        ListNode slow = head.next;
        
        while(fast!=null && fast.next!=null && fast!=slow){
            slow = slow.next;
            fast = fast.next.next;
        }
        
        if(fast ==slow ){
            //从头开始
            fast = head;
            while(fast != slow){
                fast = fast.next;
                slow = slow.next;
            }
            return fast;
        }else{
            return null;
        }
        
        
    }
}
```
 
