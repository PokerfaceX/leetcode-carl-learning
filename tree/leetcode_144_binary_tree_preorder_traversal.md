### Question 144 Binary Tree Preorder Traversal

![image-20220919212710003](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220919212710003.png)

preorder，也就是前序遍历，我们需要用中左右的方式来遍历，先记录中间节点，再去遍历左子树，再去右子树。



```java
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> list = new ArrayList<>();
        dfs(root, list);
        return list;
    }
    
    public void dfs(TreeNode root, List<Integer> ans) {
        if (root == null) {
            return;
        }
        ans.add(root.val);
        dfs(root.left, ans);
        dfs(root.right, ans);
    }
}
```

