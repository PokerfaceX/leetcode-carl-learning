### Question 701 Insert into a Binary Search Tree

![image-20230509191942782](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230509191942782.png)

这道题目比想象的简单很多很多，因为**对于一个二叉搜索树而言，插入任何一个节点，都可以在叶子节点找到它的位置**，可以在脑子里过一点，知道个就简单很多了

```java
class Solution {
    public TreeNode insertIntoBST(TreeNode root, int val) {
        if (root == null) {
            return new TreeNode(val);
        }
        if (val > root.val) {
            root.right = insertIntoBST(root.right, val); // 得用root.right来接住新创建的节点或者是原本的右孩子
        } else {
            root.left = insertIntoBST(root.left, val);
        }
        return root;
    }
}
```

