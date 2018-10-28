Given a linked list, determine if it has a cycle in it.
//快慢指针
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
    public boolean hasCycle(ListNode head) {
        if (head==null || head.next == null)return false;
        ListNode fast = head;
        ListNode slow = head;
        fast = fast.next.next;
        slow = slow.next;
        while(fast != slow && fast != null && fast.next!=null){
            fast = fast.next.next;
            slow = slow.next;
        }
        if(fast == slow){
            return true;
        }else{
            return false;
        }
    }
}
```
 
