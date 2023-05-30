### Question 100 Same Tree

![image-20230507154027072](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230507154027072.png)

这道题目如果理解了leetocode_101那么很轻松就能做出来

~~~java
class Solution {
    public boolean isSameTree(TreeNode p, TreeNode q) {
        if (p == null && q == null) {
            return true;
        } else if (p != null && q == null) {
            return false;
        } else if (p == null && q != null) {
            return false;
        } else if (p.val != q.val) {
            return false;
        }
        boolean leftTree = isSameTree(p.left, q.left);
        boolean rightTree = isSameTree(p.right, q.right);
        return leftTree && rightTree;
    }
}
~~~

