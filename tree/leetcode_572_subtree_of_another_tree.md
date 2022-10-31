### Question 572 Subtree of Another Tree

![image-20220927120302774](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220927120302774.png)

这道题目其实和第100题非常相似，我们写一个定义好的函数，用来检测两个树是不是相等的。每次遍历大的树的时候就应用这个函数来看子树是不是相等。

~~~java
class Solution {
    public boolean isSubtree(TreeNode root, TreeNode subRoot) {
        if (root == null) {
            return false;
        }
        // 如果找到了想要的子树，那么直接返回true，否则往下遍历其他节点
        if (root.val == subRoot.val && isSameTree(root, subRoot)) {
            return true;
        }
        boolean leftSub = isSubtree(root.left, subRoot);
        if (leftSub) return true; // 同理，找到了就直接返回
        boolean rightSub = isSubtree(root.right, subRoot);
        if (rightSub) return true;
        return false; // 可以取消掉上面两个if判断，然后改成leftSub || rightSub 但是这样的话会进行无意义的递归，因为即便是找到了true也还是在遍历
    }
    
    public boolean isSameTree(TreeNode p, TreeNode q) {
        if (p == null && q == null) {
            return true;
        } else if (p == null && q != null) {
            return false;
        } else if (p != null && q == null) {
            return false;
        } else if (p.val != q.val) {
            return false;
        }
        return isSameTree(p.left, q.left) && isSameTree(p.right, q.right);
    }
}
~~~

