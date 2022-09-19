### Question 160 Intersection of Two Linked List

![image-20220905215426523](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220905215426523.png)

这道题目依旧是双指针的应用，若是A指针遍历到了null那么就指向headerB，如果B指针遍历到了null，就让她指向A的入口。这两个指针早晚会指向相同的节点，这个节点可以为任意节点包括null。直接返回最终A或者B指针就好。

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        ListNode curr1 = headA;
        ListNode curr2 = headB;
        // 当两个指针同时为null的时候，也会ji
        while (curr1 != curr2) {
            if (curr1 == null) {
                curr1 = headB;
            } else {
                curr1 = curr1.next;
            }
            if (curr2 == null) {
                curr2 = headA;
            } else {
                curr2 = curr2.next;
            }
        }
        return curr1;
    }
}
```

