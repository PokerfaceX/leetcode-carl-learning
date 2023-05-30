### Question 116 Populating Next Right Pointers in Each Node

![image-20230505234035733](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230505234035733.png)

个人的做法依旧是套用层序遍历的模板，然后再每一层的循环中，让pop出来的节点指向栈顶，当遍历到这层最后一个元素的时候，让他指向null

```java

class Solution {
    public Node connect(Node root) {
        Queue<Node> queue = new LinkedList<>();
        if (root != null) {
            queue.add(root);
        }
        while (!queue.isEmpty()) {
            int size = queue.size();
            for(int i = 0; i < size; i++) {
                Node curr = queue.poll();
                if (i < size - 1) {
                    curr.next = queue.peek();
                } else {
                    curr.next = null;
                }
                if (curr.left != null) {
                    queue.add(curr.left);
                }
                if (curr.right != null) {
                    queue.add(curr.right);
                }
            }
        }
        return root;
    }
}
```

