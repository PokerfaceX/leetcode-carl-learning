### Question 145 Binary Tree Postorder Traversal

![image-20220919214447438](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220919214447438.png)

postorder，后序遍历，左右中，那么我们就需要先遍历左子树，右子树，在对中间节点进行操作。

~~~java
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> list = new ArrayList<>();
        dfs(root, list);
        return list;
    }
    
    public void dfs(TreeNode root, List<Integer> ans) {
        if(root == null) {
            return;
        }
        dfs(root.left, ans);
        dfs(root.right, ans);
        ans.add(root.val);
    }
}
~~~

