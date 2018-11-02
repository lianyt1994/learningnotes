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
    public boolean isPalindrome(ListNode head) {
        
        ListNode fast = head;
        ListNode slow = head;
        
        while( fast!=null && fast.next!=null){
            fast = fast.next.next;
            slow = slow.next;
        }
        //slow是在中间还是在右边都是可以的
        ListNode a = reverse(slow);
        while(a!=null && head!=null){
            if(a.val != head.val)return false;
            a = a.next;
            head = head.next;
        }
        //如果有一个走到空就对了
        return true;
        
    }
    
    ListNode reverse(ListNode head){
        ListNode pre = null;
        ListNode next = null;
        while(head != null){
            next = head.next;
            head.next = pre;
            pre = head;
            head = next;
        }
        return pre;
    }
}
```
