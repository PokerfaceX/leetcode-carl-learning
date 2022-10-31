### Question 236 Lowest Common Ancestor of a Binary Tree

![image-20221027225754665](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20221027225754665.png)

![image-20221027225814651](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20221027225814651.png)

这道题目一开始的时候是蒙蔽的，我猜到了它需要用后序遍历，因为我们需要从左子树和右子树返回些东西后做一点判断。其实这道题目的核心思想就是，因为后续遍历的顺序是**左右中**，那么我们就看左子树和右子树返回的东西有啥，如果都不是空，就说明是节点的祖先，如果只有一个子树包含了p或者q，那么也要返回。原因是因为需要告诉上一层至少这里发现了p或者q

```java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (root == null) {
            return null;
        }
        if (root == p || root == q) {
            return root;
        }
        TreeNode left = lowestCommonAncestor(root.left, p, q);
        TreeNode right = lowestCommonAncestor(root.right, p, q);
        if (left != null && right != null) {
            return root;
        } else if (left == null && right != null) {
            return right;
        } else if (left !=null && right == null) {
            return left;
        }
        return null;
    }
}
```

其实我一开始的时候，也没有完全理解，尤其是example2，根本不太清楚，但是仔细看了卡哥的视频就发现，example2的情况其实在我们的代码里已经覆盖了。

卡哥视频讲解的很好： https://www.bilibili.com/video/BV1jd4y1B7E2/?spm_id_from=333.788&vd_source=60e6f0aa6d18b1e267c1a770a39b7276