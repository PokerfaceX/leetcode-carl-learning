### Question 701 Insert into a Binary Search Tree

![image-20221030191217100](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20221030191217100.png)

这道题目比想象的简单很多很多，因为**对于一个二叉搜索树而言，插入任何一个节点，都可以在叶子节点找到它的位置**，那么就简单很多了

```java
class Solution {
    public TreeNode insertIntoBST(TreeNode root, int val) {
        if (root == null) {
            return new TreeNode(val);
        }
        if (root.val > val) {
            root.left = insertIntoBST(root.left, val); // 这里把上面的return的节点给接住
        } else if (root.val < val) {
            root.right = insertIntoBST(root.right, val);
        }
        return root;
    }
}
```

