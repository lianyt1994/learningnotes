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
        ListNode slow = head;
        ListNode fast = head;

        //如果走到空就说明没有交点
        while (fast!=null && fast.next!=null){
            fast = fast.next.next;
            slow = slow.next;

            //如果两个节点相等，就说明有交点，break出来
            if (fast == slow){
                ListNode slow2 = head; 
                while (slow2 != slow){
                    slow = slow.next;
                    slow2 = slow2.next;
                }
                return slow;
            }
        }
        return null;
    }
}

```
 
