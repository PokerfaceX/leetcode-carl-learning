### Question 19 Remove Nth Node From End of List

![image-20230420203348557](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230420203348557.png)

刚看到这道题目，第一个思路就是快慢指针。假设n为2，那么就先让快指针领先慢指针两步，在同时便利它们。大概是这样的逻辑，但是需要处理一下边边角角的情况。上代码

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
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode curr = head;
        ListNode forward = head;
        for(int i = 0; i < n; i++) {
            forward = forward.next;
        }
        //如果快指针遍历到了null，那么就说明我们要删除的其实是第一个节点，也就是head
        if (forward == null) {
            return head.next;
        }
        //这里之所以写成forward.next != null是因为我们需要让慢指针停留在想要shan'ch
        while (forward.next != null) {
            forward = forward.next;
            curr = curr.next;
        }
        curr.next = curr.next.next;
        return head;
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
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        curr = head
        after = head
        for i in range(0, n):
            after = after.next

        if after == None:
            return head.next

        while after.next != None:
            after = after.next
            curr = curr.next
        curr.next = curr.next.next
        return head
```

