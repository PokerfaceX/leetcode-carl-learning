### Question 110 Balanced Binary Tree

![image-20220925223002106](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220925223002106.png)

这道题目看了下卡哥的代码，但是后来感觉不是那么太好理解，所以直接看了下discussion，直接计算每一个节点的高度，这个左子树和左子树的高度差距大于1，那么这棵树就不是balanced所以让一个global variable为false

```java
class Solution {
    
    private boolean balanced = true;
    
    public boolean isBalanced(TreeNode root) {
        getHeight(root);
        return balanced;
    }
    
    public int getHeight(TreeNode root) {
        if (root == null) {
            return 0;
        }
        int leftHeight = getHeight(root.left);
        
        int rightHeight = getHeight(root.right);
        
        if (Math.abs(leftHeight - rightHeight) > 1) {
            balanced = false;
        }
        return 1 + Math.max(leftHeight, rightHeight);
    }
}
```

