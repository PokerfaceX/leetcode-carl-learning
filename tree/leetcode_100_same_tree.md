### Question 100 Same Tree

![image-20220927103405866](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220927103405866.png)

这道题目如果理解了leetocode_101那么很轻松就能做出来

~~~java
class Solution {
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

