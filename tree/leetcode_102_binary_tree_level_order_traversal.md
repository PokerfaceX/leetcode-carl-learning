### Question 102 Binary Tree Level Order Traversal

![image-20220922215127964](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220922215127964.png)

这道题目要求的是层序遍历，其实二叉树的层序遍历就是图论里面广度优先搜索bfs的一种，这种遍历是一定需要用到队列的。下面就是一个模板

```java
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> list = new ArrayList<>();
        Queue<TreeNode> queue = new LinkedList<>();
        if (root != null) {
            queue.add(root);
        }
        while (!queue.isEmpty()) {
            // 这一步其实比较关键，因为queue的size是不断变化的，所以不可以用queue.size()来当循环的条件
            int size = queue.size();
            List<Integer> tmp = new ArrayList<>();
            for(int i = 0; i < size; i++) {
                TreeNode curr = queue.poll();
                tmp.add(curr.val);
                if (curr.left != null) {
                    queue.add(curr.left);
                }
                if (curr.right != null) {
                    queue.add(curr.right);
                }
            }
            list.add(tmp);
        }
        return list;
    }
}
```

