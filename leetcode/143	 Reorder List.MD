Given a singly linked list L: L0→L1→…→Ln-1→Ln,
reorder it to: L0→Ln→L1→Ln-1→L2→Ln-2→…

You may not modify the values in the list's nodes, only nodes itself may be changed.

Example 1:

Given 1->2->3->4, reorder it to 1->4->2->3.
Example 2:

Given 1->2->3->4->5, reorder it to 1->5->2->4->3.<br>
分为三步：

找到中间节点，断开，把后半截单链表 reverse 一下，再合并两个单链表。
```java
public void reorderList(ListNode head) {
	if (head == null 
			|| head.next == null 
			|| head.next.next == null)
		return;
	
	ListNode slow = head;
	ListNode fast = head;
	// 找到中间结点
	while (fast.next != null && fast.next.next != null) {
		fast = fast.next.next;
		slow = slow.next;
	}
 
	ListNode second = slow.next;
	// 注意置空，分为两个链表
	// 第一个链表的长度大于（+1）等于第二个链表长度
	slow.next = null;
	// 反转后半链表
	second = reverseList(second);
	
	ListNode first = head;
	// 合并两个链表，画图模拟
	// 把第二个链表插在第一个链表中
	while (second != null) {
		// 暂存第一个后续结点
		ListNode next = first.next;
		first.next = second;
		second = second.next;
		first = first.next;
		first.next = next;
		first = first.next;
	}
}
 
// 就地翻转链表
private ListNode reverseList(ListNode head) {
	ListNode prev = null;
	ListNode next = null;
	while (head != null) {
		next = head.next;
		head.next = prev;
		prev = head;
		head = next;
	}
	return prev;
}
```
 
