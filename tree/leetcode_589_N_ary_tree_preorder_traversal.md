### Question 589 N-ary Tree Preorder Traversal

![image-20230506192603159](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230506192603159.png)

这道题目其实和普通的二叉树前序遍历几乎没有区别，只不过从左右子树变成了N叉树。

~~~java
class Solution {
    public List<Integer> preorder(Node root) {
        List<Integer> ans = new ArrayList<>();
        dfs(root, ans);
        return ans;
    }
		
  // 中左右
    public void dfs(Node root, List<Integer> ans) {
        if (root == null) {
            return;
        }
        // 当前层的逻辑
        ans.add(root.val);
        for(Node child: root.children) {
          // 这里告诉函数如何调用自身
          dfs(child, ans);
        }
    }
}
~~~

