### Question 110 Balanced Binary Tree

![image-20230507111850290](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230507111850290.png)

```java
class Solution {
    public boolean isBalanced(TreeNode root) {
        if (root == null) {
            return true;
        }
        int leftHeight = getHeight(root.left);
        int rightHeight = getHeight(root.right);


        return Math.abs(leftHeight - rightHeight) <= 1 && isBalanced(root.left) && isBalanced(root.right);
    }

    public int getHeight(TreeNode root) {
        if (root == null) {
            return 0;
        }
        int leftHeight = getHeight(root.left);
        int rightHeight = getHeight(root.right);

        return 1 + Math.max(leftHeight, rightHeight);
    }
}
```

这道题目一开始的时候思路有点错了，我们需要检查所有的子节点他们的高度是不是balanced的，而不是单纯的只是返回左右子树的高度，比如这种情况

```
							 1
						2		  2
          3  	    	3
        4							4 
							
```

这时候左子树和右子树的最大高度都为3但是其实这棵树不是balanced的，因为两个节点2他们的高度差大于1了



上面的代码可以过但是其实感觉有点别扭，有没有一种法子，在计算高度的时候，就已经能够知道这棵树是不是balanced的了



这道题目卡哥的代码不是很好理解，所以直接看了下discussion，直接计算每一个节点的高度，这个左子树和左子树的高度差距大于1，那么这棵树就不是balanced所以让一个global variable为false

```java
class Solution {
    private boolean balanced = true;
    
    public boolean isBalanced(TreeNode root) {
        if (root == null) {
            return true;
        }
        getHeight(root);
        return this.balanced;
    }

    public int getHeight(TreeNode root) {
        if (root == null) {
            return 0;
        }
        int leftHeight = getHeight(root.left);
        int rightHeight = getHeight(root.right);
        int height = 1 + Math.max(leftHeight, rightHeight);
        if (Math.abs(leftHeight - rightHeight) > 1) {
            this.balanced = false;
        }
        return height;
    }
}
```

