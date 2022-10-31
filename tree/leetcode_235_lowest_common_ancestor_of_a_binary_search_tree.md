### Question 235 Lowest Common Ancestor of a Binary Search Tree

![image-20221029132800009](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20221029132800009.png)

这道题目和236相比，惊人的相似，唯一不同的就是这道题目使用了二叉搜索树。如果理解了leetcode235，那么直接套用它的答案就可以直接通过，但是那样就失去了意义。



这道题目的关键就在于BST的特性，如果当前节点是在[p, q]的范围之内，就说明找到了公共祖先而且一定是最近的。

初始代码

```java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (root == null) {
            return null;
        }
        if ((root.val >= p.val && root.val <= q.val) || (root.val <= p.val && root.val >= q.val)) {
            return root;
        }
        TreeNode leftValid = lowestCommonAncestor(root.left, p, q);
        if (leftValid != null) {
            return leftValid;
        }
        TreeNode rightValid = lowestCommonAncestor(root.right, p, q);
        if (rightValid != null) {
            return rightValid;
        }
        return null;
    }
}
```



但是上面的解法，有个问题就是，没有利用到BST的特性，所以看了下卡哥的解法，确实很简洁

~~~java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        // if (root == null) {return null;} 不会出现root为空的情况，node数量至少为2而且也不会遍历到null，因为肯定会有节点在p和q的区间
        if (root.val < p.val && root.val < q.val) {
            TreeNode rightFound = lowestCommonAncestor(root.right, p, q);
            // 如果是搜索一条边，就需要用一个变量lai
            if (rightFound != null) {
                return rightFound;
            
        } else if(root.val > p.val && root.val > q.val) {
            TreeNode leftFound = lowestCommonAncestor(root.left, p, q);
            if (leftFound != null) {
                return leftFound;
            
        } 
        return root;
    }
}
~~~

可以在精简一些

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



这里的话在复习下什么时候需要接住返回值，什么时候不用

![image-20221029232737571](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20221029232737571.png)
