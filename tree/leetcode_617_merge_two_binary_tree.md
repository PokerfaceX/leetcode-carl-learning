### Question 617 Merge Two Binary Trees

![image-20230508205445976](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230508205445976.png)

这道题目其实算是比较简单的一道题目，唯一需要思考一下的点就是如何创建新的Tree。

```java
class Solution {
    public TreeNode mergeTrees(TreeNode root1, TreeNode root2) {
        if (root1 == null && root2 == null) {
            return null;
        } else if (root1 == null && root2 != null) {
            return root2;
        } else if (root1 != null && root2 == null) {
            return root1;
        }
        // 创建一个新的node并且开始构造新树的链接
        TreeNode curr = new TreeNode(root1.val + root2.val);
        curr.left = mergeTrees(root1.left, root2.left);
        curr.right = mergeTrees(root1.right, root2.right);
        return curr;
        
    }
}
```

卡哥的代码稍微简洁一些，核心逻辑就是，在root1这个树的基础上修改这个树，我认为逻辑上稍微复杂一丢丢，还是我自己的比较好懂



```java
class Solution {
    // 递归
    public TreeNode mergeTrees(TreeNode root1, TreeNode root2) {
        if (root1 == null) return root2;
        if (root2 == null) return root1;

        root1.val += root2.val;
        root1.left = mergeTrees(root1.left,root2.left);
        root1.right = mergeTrees(root1.right,root2.right);
        return root1;
    }
}
```

