### Question 206 Reverse Linked List

![image-20230420194307407](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230420194307407.png)

解决这道题目需要两个指针，一个pre(previous)，一个curr(current)，这个curr指针一开始和head指向的节点是一样的。pre则是一直指向着curr之前的节点。

上代码

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
    public ListNode reverseList(ListNode head) {
        //处理一个链表为空或者链表长度为一的边界情况
        if (head == null) {
            return head;
        } 
        ListNode pre = null, curr = head;
        while (curr != null) {
            //这里定义一个指针，用来记录curr的下一位置，不然让curr指向pre之后没法向前移动yi'bu
            ListNode after = curr.next;
            curr.next = pre;
            pre = curr;
            curr = after;
        }
        return pre;
    }
}
```

```python
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if head == None:
            return head
        prev, curr = None, head
        while curr != None:
            after = curr.next
            curr.next = prev
            prev = curr
            curr = after
        return prev
```

