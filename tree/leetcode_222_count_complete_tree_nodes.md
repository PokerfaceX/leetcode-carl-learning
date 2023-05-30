### Question 222 Count Complete Tree Nodes

![image-20230506200645855](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230506200645855.png)

这道题目的话，可以使用前序遍历，来分别计算出左子树和右子树的节点数量，在进行加一操作来得出全部的节点数量

```java
class Solution {
    public int countNodes(TreeNode root) {
        if (root == null) {
            return 0;
        }
        return 1 + countNodes(root.left) + countNodes(root.right);
    }
}
```



其实上面的方法并没有使用到完全二叉树的特性，对于完全二叉树而言，他必然会有两种情况。

情况一：就是满二叉树，情况二：最后一层叶子节点没有满。

对于情况一，可以直接用 2^树深度 - 1 来计算，注意这里根节点深度为1。

对于情况二，分别递归左孩子，和右孩子，递归到某一深度一定会有左孩子或者右孩子为满二叉树，然后依然可以按照情况1来计算。

![image-20220925215531618](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220925215531618.png)

只要同时遍历左指针和右指针，就会知道一个子树是不是满二叉树，那样的话就能通过公式直接计算出节点的数量，而不用遍历中间的那些节点，所以时间复杂度会低一点点

```java
class Solution {
    public int countNodes(TreeNode root) {
        if (root == null) {
            return 0;
        }
        TreeNode leftP = root.left;
        TreeNode rightP = root.right;
        int leftDepth = 0, rightDepth = 0;
        
        // 看以当前节点为根节点的情况下，当前子树是不是一个满二叉树
        while (leftP != null) {
            leftDepth++;
            leftP = leftP.left;
        }
        while (rightP != null) {
            rightDepth++;
            rightP = rightP.right;
        }
        
        if (leftDepth == rightDepth) {
            return (2 << leftDepth) - 1; // 满二叉树的公式2^n - 1
        }
        // 上面完成了递归三部曲中的第二步，找到zhong'zhi'ti
        int numOfRight = countNodes(root.right);
        int numOfLeft = countNodes(root.left);
        return 1 + numOfLeft + numOfRight;
    }
}
```

