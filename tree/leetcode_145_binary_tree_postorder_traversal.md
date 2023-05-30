### Question 145 Binary Tree Postorder Traversal

![image-20230504211124539](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230504211124539.png)

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

再次强调，后序遍历的顺序是左右中

在前序遍历的时候，我们的顺序是中左右，那么我们在微调一下前面前序遍历的迭代方式，使其变成中右左，那么可以看出，我们现在只要反转一下答案数组，就得到答案。

```java
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        Stack<TreeNode> stack = new Stack<>();
        stack.add(root);
        List<Integer> ans = new ArrayList<>();
        while (!stack.isEmpty()) {
            TreeNode curr = stack.pop();
            if (curr != null) {
                ans.add(curr.val);
                stack.add(curr.left); // 上下顺序调换
                stack.add(curr.right);
            }
            
        }
        Collections.reverse(ans); // 把答案反转
        return ans;
    }
    
    
}
```

