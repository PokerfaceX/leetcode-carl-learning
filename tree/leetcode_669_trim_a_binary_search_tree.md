### Question 669 Trim a Binary Search Tree

![image-20221031214218520](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20221031214218520.png)

一开始想直接复刻 leetcode_450的解法，但是发现不管用

```java
class Solution {
    public TreeNode trimBST(TreeNode root, int low, int high) {
        if (root == null) {
            return null;
        }
        // 写到这里就蒙了，因为不知道该怎么接住
        if (root.val < low) {
            
        }
    }
    
    public TreeNode deleteNode(TreeNode curr) {
        if (curr.left != null && curr.right == null) {
            return curr.left;
        } else if (curr.left == null && curr.right != null) {
            return curr.right;
        } else {
            TreeNode tmp = curr.right;
            while (tmp.left != null) {
                tmp = tmp.left;
            }
            tmp.left = curr.left;
            return curr.right;
        }
        return null;
    }
}
```



第二种想法:

```java
class Solution {
    public TreeNode trimBST(TreeNode root, int low, int high) {
        if (root == null) {
            return null;
        }
        if (root.val < low) {
            
            if (root.right != null && root.right.val >= low) {
                return root.right;
            } else {
                return null;
            }
        }
        if (root.val > high) {
            if (root.left != null && root.left.val <= high) {
                return root.left;
            } else {
                return null;
            }
        }
        root.left = trimBST(root.left, low, high);
        root.right = trimBST(root.right, low, high);
        return root;
    }
}
```

上面的做法也不行，参考这个树

![image-20221101084650744](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20221101084650744.png)

如果按照上面的做法，在根节点的时候，发现比high大，然后看了左子树也比1大，所以直接return了null但是其实很明显这样是错的



**正确做法**

```java
class Solution {
    public TreeNode trimBST(TreeNode root, int low, int high) {
        if (root == null) {
            return null;
        }
        if (root.val < low) {
        // 解决了上面的情况，直接不断的进行遍历
            return trimBST(root.right, low, high);
        }
        if (root.val > high) {
            return trimBST(root.left, low, high);
        }
        root.left = trimBST(root.left, low, high); // 
        root.right = trimBST(root.right, low, high);
        return root;
    }
}
```



上面之所以能删除节点，是因为直接把被修剪之后的子树返还给了父亲节点。
