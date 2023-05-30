### Question 669 Trim a Binary Search Tree

![image-20221031214218520](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20221031214218520.png)

这道题目需要一种很巧妙的做法，我们其实没有动态的去删除节点，而是单纯的把符合区域的节点返回给上一层

**正确做法**

```java
class Solution {
    public TreeNode trimBST(TreeNode root, int low, int high) {
        if (root == null) {
            return null;
        }
        if (root.val < low) {
          // 得到一个符合规定的右子树
            TreeNode rightValidTree = trimBST(root.right, low, high);
            return rightValidTree;
        } else if (root.val > high) {
          // 得到一个符合规定的左子树
            TreeNode leftValidTree = trimBST(root.left, low, high);
            return leftValidTree;
        }
        root.left = trimBST(root.left, low, high);
        root.right = trimBST(root.right, low, high);
        return root;
    }
}
```



上面之所以能删除节点，是因为直接把被修剪之后的子树返还给了父亲节点。

区间为[3, 7]

![image-20230509210635806](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230509210635806.png)

比如上面这个例子，我们的0不符合规矩，那么比0还小的数值肯定低于L，那么就去看0的右子树，一个个检查，发现3符合规矩，那么在看3的左右子树，发现2不符合条件，那么我们这时候就会去遍历2的右子树，因为是空所有就会向上一层返回空，那么3的左孩子就为空了，如此以来我们就实现了2节点的**"删除"**，并且最终给节点7返回的是节点3，也就实现了节点0的删除
