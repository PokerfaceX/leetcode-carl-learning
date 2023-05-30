### Question 538 Convert BST to Greater Tree

![image-20230510224014188](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230510224014188.png)

这道题目一开始想的时候没什么头绪，但是仔细想了想发现，其实就是使用右中左的遍历方式就可以了，同时我们使用一个prev指针来记录指针的数值，那么每次就加到当前的节点就可以了



```java
class Solution {

    TreeNode prev = null;

    public TreeNode convertBST(TreeNode root) {
        if (root == null) {
            return null;
        }
        convertBST(root.right);
        if (prev != null) {
            root.val += prev.val;
        }
        prev = root;
        convertBST(root.left);
        return root;
    }
}
```



下面的话大同小异，只是把prev当成一个数值使用

~~~java
class Solution {
    
    int prev = 0; // 用来记录上一个数值，因为是逐渐累加的，需要一个变量来记录上一个累计的最大值，这里可以用TreeNode来代替但是还得处理空指针的情况，不是很方便
    
    public TreeNode convertBST(TreeNode root) {
        traversal(root);
        return root;
    }
    
    public void traversal(TreeNode curr) {
        if (curr == null) {
            return;
        }
        // 右
        traversal(curr.right);
        // 中
        curr.val = curr.val + prev;
        prev = curr.val;
        // 左
        traversal(curr.left);
        
    }
}
~~~

