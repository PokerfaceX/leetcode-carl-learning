### 	Question 101 Symmetric Tree

![image-20220924160624179](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220924160624179.png)

对于这道题目而言，问的尽管是二叉树是不是对称的，但是为了解决问题，其实我们需要知道左右子树是不是相互反转的，用人话来说，就是分别比较左子树的内测节点和外侧节点相同不相同。

每次做二叉树递归题目的时候，都需要思考，应该用什么遍历顺序。在这里面，对于根节点而言，只要左子树和右子树是相互反转的，那么整个树就是对称的。所以其实我们需要同时遍历两棵树。

```java
class Solution {
    public boolean isSymmetric(TreeNode root) {
        return dfs(root.left, root.right);
    }
    
    // 第一步，确认返回值和参数
    public boolean dfs(TreeNode left, TreeNode right) {
    // 第二部确认终止条件
        if (left == null && right == null) {
            return true;
        } else if (left == null && right != null) {
            return false;
        } else if (left != null && right == null) {
            return false;
        } else if (left.val != right.val) {
            return false;
        }
        // 第三步确认单层逻辑
        boolean leftSymmetric = dfs(left.left, right.right); // 左
        boolean rightSymmetric = dfs(left.right, right.left); // 右
        
        return leftSymmetric && rightSymmetric; // 中
        
    }
}
```

当一个中间节点，需要左子树和右子树的信息的时候，就只能使用后序遍历