### Question 203 Remove Linked List Elements

![image-20230418204928471](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230418204928471.png)

如果只是在linkedlist里面删除一次删除操作，代码相对简单，但是这里涉及到的点是多次的删除操作。

在这个题目里面，我们额外定义了一个虚拟头节点，叫dummy，为什么需要这么一个虚拟头节点呢？其实主要是为了处理head的逻辑，若是删除的点是head的话，那么我们需要一个额外的if语句来修改链表，来移动head指针，而有了这个dummy结点之后，我们省下了这个多余的if语句。

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
    public ListNode removeElements(ListNode head, int val) {
        ListNode dummy = new ListNode(-1, head);
        ListNode pre = dummy, curr = head;
        while (curr != null) {
            //可以看到，当进行了删除的时候，我们只需要移动一个指针(curr)，若是没有进行删除操作，那么就需要同时移动两个指针。
            if (curr.val == val) {
                pre.next = curr.next;
            } else {
                pre = curr;
            } 
            
            curr = curr.next;
            
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
    def removeElements(self, head: Optional[ListNode], val: int) -> Optional[ListNode]:
        dummyNode = ListNode(-1, head)
        curr = dummyNode
        while curr.next != None:
            if curr.next.val == val:
                curr.next = curr.next.next
            else:
                curr = curr.next
        return dummyNode.next

```

