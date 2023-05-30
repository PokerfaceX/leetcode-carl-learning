### Question 226 Invert Binary Tree

![image-20230506192235610](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230506192235610.png)

 对于这道题目而言，可以使用前序遍历，对于每一个中间节点，进行左右孩子的交换

```java
class Solution {
    public TreeNode invertTree(TreeNode root) {
        if (root == null) {
            return root;
        }
        TreeNode tmp = root.right;
        root.right = root.left;
        root.left = tmp;
        invertTree(root.left);
        invertTree(root.right);
        return root;
    }
}
```

