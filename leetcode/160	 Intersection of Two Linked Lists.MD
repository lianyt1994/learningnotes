Write a program to find the node at which the intersection of two singly linked lists begins.


For example, the following two linked lists:

A:          a1 → a2
                   ↘
                     c1 → c2 → c3
                   ↗            
B:     b1 → b2 → b3
begin to intersect at node c1.


Notes:

If the two linked lists have no intersection at all, return null.
The linked lists must retain their original structure after the function returns.
You may assume there are no cycles anywhere in the entire linked structure.
Your code should preferably run in O(n) time and use only O(1) memory.
<br>
常用方法
```java
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        if(headA==null || headB==null) return null;
        
        ListNode p = headA;
        ListNode q = headB;
        int pcount = 0;
        int qcount = 0;
        while(p.next != null || q.next != null) {
            if(p == q) return p;
            if(p.next != null) p = p.next; else ++qcount;
            if(q.next != null) q = q.next; else ++pcount;
        }
        if(p != q) return null;
        p = headA;
        q = headB;
        
        //pcount和qcount就是二者之差
        while(pcount-- != 0) {
            p = p.next;
        }
        while(qcount-- != 0) {
            q = q.next;
        }
        
        while(p != q) {
            p = p.next;
            q = q.next;
        }
        return p;
    }
```
//这个方法很6
```java
public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
    //boundary check
    if(headA == null || headB == null) return null;
    
    ListNode a = headA;
    ListNode b = headB;
    
    //不断循环，一定可以都走到同一点或者null
    while( a != b){
    	//for the end of first iteration, we just reset the pointer to the head of another linkedlist
        a = a == null? headB : a.next;
        b = b == null? headA : b.next;    
    }
    
    return a;
}
```
