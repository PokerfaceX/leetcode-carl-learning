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



对于这道题目，我们依旧可以用过手动调用栈来实现

```java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> ans = new ArrayList<>();
        Stack<TreeNode> stack = new Stack<>();
        TreeNode curr = root;
        // 当两个条件有一个被满足就可以运行循环
        while (!stack.isEmpty() || curr != null) {
            // 先遍历到最左侧
            if (curr != null) {
                stack.add(curr);
                curr = curr.left;
            } else {
                // 这时候指针一定是null，那么就说明我们到了当前的最左侧，pop一下，加入到答案数组里，z
                curr = stack.pop();
                ans.add(curr.val);
                curr = curr.right;
            }
        }
        return ans;
    }
}
```

