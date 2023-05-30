### Question 141 Linked List Cycle

![image-20230426223624040](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230426223624040.png)



这道题目的核心就在快慢指针，我们定义一个慢指针，一次只走一步，快指针，一次走两步。

这样的话当两个指针同时在环内的时候，对于慢指针而言，快指针其实就相当于一次一步的在靠近它，迟早会相遇。但是我们不可以让快指针一次走三步，因为那样的话它就是两步两步的靠近慢指针，是有可能直接跳过慢指针的位置的，从而导致它们从不相遇。

```python
class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        slow, fast = head, head
        while fast != None and fast.next != None:
            slow = slow.next
            fast = fast.next.next
            if slow == fast:
                return True
        return False
```

