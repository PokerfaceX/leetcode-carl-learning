### Question 700 Search In a Binary Search Tree

![image-20221024211013400](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20221024211013400.png)

这道题目的话其实一开始做的时候并没有考虑二叉搜索树的特性，只是当作普通的树来做的。**只有寻找某一条边（或者一个节点）的时候，递归函数会有bool类型的返回值。**

```java
class Solution {
    public TreeNode searchBST(TreeNode root, int val) {
        if (root == null) {
            return null;
        }
        if (root.val == val) {
            return root;
        }
        TreeNode res1 = searchBST(root.left, val);
        // 找到了就直接返回
        if (res1 != null) {
            return res1;
        }
        TreeNode res2 = searchBST(root.right, val);
        if (res2 != null) {
            return res2;
        }
        return null;
    }
}
```

但是上面的时间复杂度为O(N)，N就是节点的数量



进行一下优化，充分利用二叉搜索树的特性
~~~java
class Solution {
    public TreeNode searchBST(TreeNode root, int val) {
        if (root == null) {
            return null;
        }
        if (root.val == val) {
            return root;
        }
        TreeNode result = null;
        if (root.val > val) {
           result = searchBST(root.left, val); 
        } 
        if (root.val < val) {
            result = searchBST(root.right, val);
        }
        return result;
    }
}
~~~

代码的时间复杂度为O(log(N))