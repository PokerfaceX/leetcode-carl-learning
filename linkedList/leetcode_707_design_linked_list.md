#### Question 707 Design Linked List

![image-20220629222658299](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220629222658299.png)

一下方法用了虚拟头节点，一开始画的时候容易蒙，原因就是如果给的index是3，那么我们要操作的index就会是4，这是因为虚拟头节点的存在

```java
// 自定义一个节点的类
class ListNode {
    int val;
    ListNode next;
    
    public ListNode(int val) {
        this.val = val;
    }
    
    public ListNode(int val, ListNode newNode) {
        this.val = val;
        this.next = newNode;
    } 
    
}

class MyLinkedList {
    
    ListNode header;
    int numOfNodes;
    
    public MyLinkedList() {
        this.numOfNodes = 0; //可以看到虚拟头节点的存在不会影响整个链表的长度
        this.header = new ListNode(-111); // 不管发生什么情况，我们都不需要管header指针，这也是虚拟头节点的好处
    }
    
    public int get(int index) {
        if (index < 0 || index > numOfNodes - 1) {
            return -1;
        }
        ListNode curr = header;
        int i = 0;
        // 这个遍历的数字index + 1挺让人发懵的，但是其实拿着笔画一画就好
        while (i < index + 1) {
            curr = curr.next;
            i++;
        }
        return curr.val;
    }
    
    public void addAtHead(int val) {
        addAtIndex(0, val);
    }
    
    public void addAtTail(int val) {
        addAtIndex(this.numOfNodes, val);
    }
    
    public void addAtIndex(int index, int val) {
        if (index > numOfNodes || index < 0) {
            return;
        }
        ListNode curr = header;
        // 拿个纸笔画一画，会发现因为虚拟头节点的存在，刚好会遍历到要添加的位置之前的位置，非常方便进行插入
        for(int i = 0; i < index; i++) {
            curr = curr.next;
        }
        ListNode newNode = new ListNode(val, curr.next);
        curr.next = newNode;
        this.numOfNodes++;
    }
    
    public void deleteAtIndex(int index) {
        if (index < 0 || index >= this.numOfNodes) {
            return;
        }
        ListNode curr = header;
        // 拿个纸笔画一画，会发现因为虚拟头节点的存在，刚好会遍历到要删除的地方之前的位置，删除
        for(int i = 0; i < index; i++) {
            curr = curr.next;
        }
        curr.next = curr.next.next;
        this.numOfNodes--;
        
    }
}

/**
 * Your MyLinkedList object will be instantiated and called as such:
 * MyLinkedList obj = new MyLinkedList();
 * int param_1 = obj.get(index);
 * obj.addAtHead(val);
 * obj.addAtTail(val);
 * obj.addAtIndex(index,val);
 * obj.deleteAtIndex(index);
 */
```

其实我个人认为这道题恶心就恶心在while循环中同时递增指针和变量i，这样的话非常容易出现过界的情况，另外就是head指针的修改，一定要注意。