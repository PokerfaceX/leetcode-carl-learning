### Question 450 Delete Node in a BST

![image-20230509200517097](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230509200517097.png)

这道题目算是蛮难的一道题，但是考的概率非常高。

当我们删除一道节点时，会有以下五种可能

1. 我们要删除的节点不存在
2. 要删除的节点是一个叶子节点
3. 要删除的节点有子节点，但是左子树为空，右子树不为空
4. 要删除的节点有子节点，但是左子树不为空，右子树为空
5. 要删除的节点，左右节点都不为空



上面的五种情况，其实我们都需要分别加入一个if语句来判断



```java
class Solution {
    public TreeNode deleteNode(TreeNode root, int key) {
        // 当我们遍历到了null节点就说明要删除的节点不存在，原因就是因为这是一个二叉搜索树，我们会不断的向左或者向右有逻辑性的遍历这个二叉树
        if (root == null) {
            return null;
        }
        if (root.val == key) {
            // 叶子节点的情况，直接返回null就可以了，因为null是返还给父亲节点的，把父亲节点的左节点或者是右节点变成null就是删除了
            if (root.left == null && root.right == null) {
                return null;
            // 当左子树不为空，右子树为空，那么就直接把左子树返回就可以了
            } else if (root.left != null && root.right == null) {
                return root.left;
            // 跟上面逻辑一样，但是把右子树返回
            } else if (root.left == null && root.right != null) {
                return root.right;
            // 我们把左子树放到右子树的最小节点的左面就可以了，不会打破二叉搜索树的特性
            } else {
                TreeNode tmp = root.right;
                while (tmp.left != null) {
                    tmp = tmp.left;
                }
                tmp.left = root.left;
                return root.right;
            }
        } else if (root.val < key) {
            root.right = deleteNode(root.right, key);
        } else {
            root.left = deleteNode(root.left, key);
        }
        return root;
    }
}
```

https://programmercarl.com/0450.%E5%88%A0%E9%99%A4%E4%BA%8C%E5%8F%89%E6%90%9C%E7%B4%A2%E6%A0%91%E4%B8%AD%E7%9A%84%E8%8A%82%E7%82%B9.html#%E9%80%92%E5%BD%92

上面有图解