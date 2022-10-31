### Question 98 Validate Binary Search Tree

![image-20221024224437115](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20221024224437115.png)

一开始的时候，我想成了后续遍历并且写出了类似的代码![image-20221024224517816](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20221024224517816.png)

这样写肯定不行，所以比较简单的做法就是，用中序遍历，因为对于一个二叉搜索树而言，如果使用了中序遍历就可以把数组从小到大排开。

```java
class Solution {
    
    List<Integer> list = new ArrayList<>();
    
    public boolean isValidBST(TreeNode root) {
        dfs(root);
        for(int i = 0; i < list.size() - 1; i++) {
            if (list.get(i) > list.get(i + 1)) {
                return false;
            }
        }
        return true;
        
    }
    
    public void dfs(TreeNode root) {
        if (root == null) {
            return;
        }
        dfs(root.left);
        list.add(root.val);
        dfs(root.right);
    }
}
```

下面的话使用了一个指针来记录之前的节点，同时在进行中序遍历，那样的话就可以不使用额外的内存空间，而直接进行比较



~~~java
class Solution {
    
    TreeNode prev = null;
    
    public boolean isValidBST(TreeNode root) {
        if (root == null) {
            return true;
        }
        boolean leftValid = isValidBST(root.left);
        if (prev != null && prev.val >= root.val) {
            return false;
        }
        prev = root;
        boolean rightValid = isValidBST(root.right);
        return leftValid && rightValid;
    }
}
~~~

