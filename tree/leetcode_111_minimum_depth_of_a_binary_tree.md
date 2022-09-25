### Question 111 Minimum Depth of Binary Tree

![image-20220923210632297](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220923210632297.png)

这是唯一一道有一点难点的题目了，其实一开始看的时候对于如何找到最小深度可能会有点懵逼，但是仔细想象的话就会发现，当你遍历到第一个叶子节点的时候，其实就说明你遍历到了深度最浅的叶子节点，那也就是这道题目追求的最小深度

```java
class Solution {
    public int minDepth(TreeNode root) {
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
                if (curr.left == null && curr.right == null) {
                    return layer;
                }
                if (curr.left != null) {
                    queue.add(curr.left);
                }
                if (curr.right != null) {
                    queue.add(curr.right);
                }
            }
        }
        return 0;
    }
}
```



这道题目依旧可以用递归法来解决，尽管题目问的是最小深度，最小的深度就是从根节点到最近的叶子节点的距离。其实这也是等同于最小的高度，那这么一看，和leetcode104题几乎是一摸一样的，确实，但是仅仅把max改成会min就会漏掉下面这个情况。下面这种情况，最小深度不是1而是3

![image-20220925211741929](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220925211741929.png)



~~~java
class Solution {
    public int minDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }
        // 处理上面的情况
        if (root.left == null && root.right != null) {
            return 1 + minDepth(root.right);
        }
        // chu'li'shang
        if (root.left != null && root.right == null) {
            return 1 + minDepth(root.left);
        }
        int leftHeight = minDepth(root.left);
        int rightHeight = minDepth(root.right);
        
        return 1 + Math.min(leftHeight, rightHeight);
    }
}
~~~

