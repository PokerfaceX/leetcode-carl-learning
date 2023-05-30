### Question 117 Populating Next Right Pointers in Each Node II

![image-20230505235449624](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230505235449624.png)

和leetcode 116题没有任何的区别，一样的代码一样的味道

```java
class Solution {
    public Node connect(Node root) {
        Queue<Node> queue = new LinkedList<>();
        if (root == null) {
            return null;
        }
        queue.add(root);
        while (!queue.isEmpty()) {
            int size = queue.size();
            for(int i = 0; i < size; i++) {
                Node curr = queue.poll();
                if (i == size - 1) {
                    curr.next = null;
                } else {
                    curr.next = queue.peek();
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

