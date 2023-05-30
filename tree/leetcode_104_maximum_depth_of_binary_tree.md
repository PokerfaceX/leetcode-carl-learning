### Question 104 Maximum Depth Of Binary Tree

![image-20230505235758994](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230505235758994.png)

还是在套用树的bfs遍历模板，只要在层序遍历每一层之前，用一个变量来记录层数就好了

```jav
class Solution {
    public int maxDepth(TreeNode root) {
        Queue<TreeNode> queue = new LinkedList<>();
        if (root != null) {
            queue.add(root);
        }
        int layer = 0;
        while (!queue.isEmpty()) {
            int size = queue.size();
            layer++;
            for(int i = 0; i < size; i++) {
                TreeNode curr = queue.poll();
                if (curr.left != null) {
                    queue.add(curr.left);
                }
                if (curr.right != null) {
                    queue.add(curr.right);
                }
            }
        }
        return layer;
    }
}
```

其实这道题目，更多的是用DFS来解决问题，但是得先了解一下一个树的高度(height)和深度(depth)的区别



深度：根节点到当前节点的距离，depth

高度:  从当前节点到叶子节点的最远距离，height



求高度的时候，我们用的其实就是后续遍历因为在计算高度的时候，我们是从下也就是叶子节点往上去计数的

而求深度的时候，我们是要用前序遍历的，因为我们要从根节点开始操作。



对于这道题目而言，尽管问的是最大的深度，但是最大的深度会等于最大的高度，所以我们只需要通过后续遍历来求最大高度就可以得到题解

```java
class Solution {
    public int maxDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }
        int leftHeight = maxDepth(root.left); // 左
        int rightHeight = maxDepth(root.right); // 右
        
        int height = 1 + Math.max(leftHeight, rightHeight); // 中
        return height;
      // return 1 + (leftHeight > rightHeight ? leftHeight : rightHeight);
    }
}
```

上面使用了后续遍历，也是最常规的递归写法，对于怎么调用当前函数而完成递归而言，我们只需要知道，当我们得到了左子树的高度和右子树的高度之后，那么当前节点的高度就是1 + 这两个高度的最大值就行，不用去想象整个递归的过程
