### Question 142 Linked List Cycle II

![image-20230426223654405](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230426223654405.png)

这道题目，跟之前的141题非常相像，做法也是类似的，但是多了一点点改动，我们要找到具体环的入口。

我们通过数学公式证明了，快指针与慢指针相遇的点到环入口的距离和头节点到换入口的距离，其实是一样的。数学方面的东西就不讲了，直接上代码



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
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
            if (slow == fast) {
                ListNode tmp = head;
                ListNode tmp2 = fast;
                while (tmp != tmp2) {
                    tmp = tmp.next;
                    tmp2 = tmp2.next;
                }
                return tmp;
            }
        }
        // 当fast或者fast的下一个位置等于null就说明这个链表是没有环的
        return null;
    }
}
```

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def detectCycle(self, head: Optional[ListNode]) -> Optional[ListNode]:
        slow, fast = head, head
        while fast != None and fast.next != None:
            slow = slow.next
            fast = fast.next.next
            if slow == fast:
                tmp1 = head
                tmp2 = slow
                while tmp1 != tmp2:
                    tmp1 = tmp1.next
                    tmp2 = tmp2.next
                return tmp1
        return None
```

