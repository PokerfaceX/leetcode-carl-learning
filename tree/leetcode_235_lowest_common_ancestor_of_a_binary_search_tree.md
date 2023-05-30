### Question 235 Lowest Common Ancestor of a Binary Search Tree

![image-20230509190136214](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230509190136214.png)

这道题目和236相比，惊人的相似，唯一不同的就是这道题目使用了二叉搜索树。如果理解了leetcode235，那么直接套用它的答案就可以直接通过，但是那样就失去了意义。



这道题目的关键就在于BST的特性，如果当前节点是在[p, q]的范围之内，就说明找到了公共祖先而且一定是最近的。

初始代码：

这道题目有个知识点就是如果root的数值在p和q之间就说明他肯定是common ancestor，这是二叉树的特性。所以如果数值同时大于p和q就往左侧搜索，如果小于p和q就往右侧搜索，都不满足就说明肯定是在这两个数值之间，inclusive

~~~java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        TreeNode curr = root;
        while (curr != null) {
            if (curr.val < p.val && curr.val < q.val) {
                curr = curr.right;
            } else if (curr.val > p.val && curr.val > q.val) {
                curr = curr.left;
            } else {
                return curr;
            }
        }
        return curr;
    } 
}
~~~

递归法

```java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        // if (root == null) {return null;}
        if (root.val < p.val && root.val < q.val) {
            return lowestCommonAncestor(root.right, p, q);
        } else if(root.val > p.val && root.val > q.val) {
            return lowestCommonAncestor(root.left, p, q);
        } 
        return root;
    }
}
```
