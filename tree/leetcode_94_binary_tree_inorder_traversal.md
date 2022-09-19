### Question 94 Binary Tree Inorder Traversal

![image-20220919213556500](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220919213556500.png)

inorder，也就是中序遍历，实施的是左中右的遍历方式，先把所有的左子树遍历完，在添加中间节点的数值，在开始遍历右子树



```java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> list = new ArrayList<>();
        traversal(root, list);
        return list;
    }
    
    public void traversal(TreeNode root, List<Integer> list) {
        if (root == null) {
            return;
        }
        traversal(root.left, list);
        list.add(root.val);
        traversal(root.right, list);
    }
}
```

