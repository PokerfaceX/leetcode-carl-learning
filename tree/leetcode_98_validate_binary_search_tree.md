### Question 98 Validate Binary Search Tree

![image-20230508210938425](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230508210938425.png)

一开始陷入了一个误区，我只是在单纯的单纯的每一个节点，他们左节点小于他，右节点大于它，但是这样行不通，因为我们需要保证**左子树所有节点小于中间节点**，**右子树所有节点大于中间节点**



这道题目涉及到了一个知识点，对于一个二叉搜索树而言，他的**遍历必然是生序的**

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

