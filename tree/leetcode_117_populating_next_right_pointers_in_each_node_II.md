### Question 117 Populating Next Right Pointers in Each Node II

![image-20220923205702689](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220923205702689.png)

和leetcode 116题没有任何的区别，一样的代码一样的味道

```java
class Solution {
    public Node connect(Node root) {
        Queue<Node> queue = new LinkedList<>();
        if (root != null) {
            queue.add(root);
        }
        while (!queue.isEmpty()) {
            int size = queue.size();
            for(int i = 0 ; i < size; i++) {
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

