### Question 2 Add Two Numbers

![image-20220910092916256](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220910092916256.png)

其实这道题目也需要用到双指针，同时遍历两个链表，找到他们的和并且找到carryOver，上代码更容易理解

````java
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

 // 初始代码
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode dummyNode = new ListNode(-1);
        ListNode pointer = dummyNode;
        int carryOver = 0;
        ListNode curr1 = l1;
        ListNode curr2 = l2;
        while (curr1 != null && curr2 != null) {
            // 有可能 curr1 == 7, curr2 == 2, carryOver = 1,以此来进一位
            int value = (curr1.val + curr2.val+ carryOver) % 10;
            pointer.next = new ListNode(value);
            pointer = pointer.next;
            if (curr1.val + curr2.val + carryOver >= 10) {
                carryOver = 1;
            } else {
                carryOver = 0;
            }
            curr1 = curr1.next;
            curr2 = curr2.next;
        }
        // 当其中一个链表为null的时候，继续遍历剩余的一个链表
        while (curr1 != null) {
            int value = (curr1.val + carryOver) % 10;;
            pointer.next = new ListNode(value);
            
            if (curr1.val + carryOver >= 10) {
                carryOver = 1;
            } else {
                carryOver = 0;
            }
            
            curr1 = curr1.next;
            pointer = pointer.next;
            
        }
        while (curr2 != null) {
            int value = (curr2.val + carryOver) % 10;;
            pointer.next = new ListNode(value);
            
            if (curr2.val + carryOver >= 10) {
                carryOver = 1;
            } else {
                carryOver = 0;
            }
            
            curr2 = curr2.next;
            pointer = pointer.next;
            
        }
        // 如果还有carryover，还得再加一位,比如99 + 1
        if (carryOver == 1) {
            pointer.next = new ListNode(1);
        }
        return dummyNode.next;
        
    }
}
````



上面的代码逻辑其实比较清晰，但是代码有点冗余，且重复性比较大，所以看了下dicuss，发现了一个神仙题解

```java
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode dummyNode = new ListNode(-1);
        ListNode pointer = dummyNode;
        int c = 0; // 神来之笔
        ListNode curr1 = l1;
        ListNode curr2 = l2;
        while (curr1 != null || curr2 != null || c > 0) {
            if (curr1 != null) {
                c += curr1.val;
                curr1 = curr1.next;
            }
            if (curr2 != null) {
                c += curr2.val;
                curr2 = curr2.next;
            }
            // 无论curr1 + curr2等于多少，node的数值肯定是c%10的数值
            pointer.next = new ListNode(c % 10);
            // 如果c是10-19之间的数值，下次加法就会带上"carryrover"
            c = c / 10;
            pointer = pointer.next;
        }
       
        return dummyNode.next;
        
    }
}
```

