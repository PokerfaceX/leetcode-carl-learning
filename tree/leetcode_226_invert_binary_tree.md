### Question 226 Invert Binary Tree

![image-20220924130829739](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220924130829739.png)

 对于这道题目而言，可以使用前序遍历，对于每一个中间节点，进行左右孩子的交换

```java
class Solution {
    public TreeNode invertTree(TreeNode root) {
        if(root == null) {
            return null;
        }
        TreeNode tmp = root.left;
        root.left = root.right;
        root.right = tmp;
        invertTree(root.left);
        invertTree(root.right);
        return root; // 这个返回值只是用来让函数结束，并没有
    }
}
```

