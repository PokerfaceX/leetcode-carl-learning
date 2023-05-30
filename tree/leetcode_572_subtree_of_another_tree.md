### Question 572 Subtree of Another Tree

![image-20230507153552143](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230507153552143.png)

这道题目其实和第100题非常相似，我们写一个定义好的函数，用来检测两个树是不是相等的。每次遍历大的树的时候就应用这个函数来看子树是不是相等。

~~~java
class Solution {
    public boolean isSubtree(TreeNode root, TreeNode subRoot) {
        if (root == null) {
            return false;
        }
        // 以当前节点为基准，检查两个子树是不是一样的树
        if (isSameTree(root, subRoot)) {
            return true;
        }
        // 看看左子树和subroot一不一样，如果一样的话直接返回true，可以节省没意义的递归
        if (isSubtree(root.left, subRoot)) {
            return true;
        }
        if (isSubtree(root.right, subRoot)) {
            return true;
        }

        return false;
    }
		
  // 用来判断两个树是不是想等的函数
    public boolean isSameTree(TreeNode root, TreeNode subRoot) {
        if (root == null && subRoot == null) {
            return true;
        } else if (root == null && subRoot != null) {
            return false;
        } else if (root != null && subRoot == null) {
            return false;
        } else if (root.val != subRoot.val) {
            return false;
        }
        return isSameTree(root.left, subRoot.left) && isSameTree(root.right, subRoot.right);
    }
}
~~~

