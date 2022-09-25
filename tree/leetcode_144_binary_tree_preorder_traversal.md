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



第二种解法：不管是任何递归，其本质上都是栈的调用，所以对于任何可以使用递归来解决的题目，我们都可以手动创建一个栈来解决问题



前序遍历的顺序是中左右，那么我们可以创建一个栈，我们先放入中间节点的数值，在放入右侧节点，再放入左侧节点，为什么不是先放左再放右呢？因为出栈的时候我们保持先左在右的顺序，那么按照栈后进先出的原则，左侧的节点会被优先pop出去

```java
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        Stack<TreeNode> stack = new Stack<>();
        stack.add(root);
        List<Integer> ans = new ArrayList<>();
        while (!stack.isEmpty()) {
            TreeNode curr = stack.pop();
            if (curr != null) {
                ans.add(curr.val);
                stack.add(curr.right);
                stack.add(curr.left);
            }
            
        }
        return ans;
    }
    
    
}
```



