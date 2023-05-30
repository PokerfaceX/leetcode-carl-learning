### Question 24 Swap Node in Pairs

![image-20230420201748390](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230420201748390.png)

这道题目乍一看，可能会比较蒙蔽，但是其实方法也非常明显，Carl哥的图片其实就表达的很好了

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
    public ListNode swapPairs(ListNode head) {
        ListNode dummy = new ListNode(-1, head);
        ListNode curr = dummy; // 老样子，虚拟头节点用来避免head相关的逻辑
        // 要两两操作指针，所以要保证，curr的后面和curr的后面的后面都不是null
        while (curr.next != null && curr.next.next != null) {
            ListNode after = curr.next.next.next; // 所谓的第三个节点
            
            ListNode first = curr.next;
            ListNode second = curr.next.next;
            
            curr.next = second;
            second.next = first;
            first.next = after;
            
            curr = first; // 画图就直观了
        }
        return dummy.next;
    }
}
```

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def swapPairs(self, head: Optional[ListNode]) -> Optional[ListNode]:
        dummy = ListNode(-1, head)
        curr = dummy
        while curr.next and curr.next.next:
            after = curr.next.next.next

            first = curr.next
            second = curr.next.next

            curr.next = second
            second.next = first
            first.next = after

            curr = first
        return dummy.next
```



