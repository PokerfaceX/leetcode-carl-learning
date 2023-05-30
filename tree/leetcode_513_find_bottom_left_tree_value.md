### Question 513 Find Bottom Left Tree Value

![image-20230507161841451](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230507161841451.png)做任何一道题目之前，都要保证我们完全理解了题目，这道题问的是最后一行的最左值，而不是单单整个树里面最左侧的值，这一点要搞清楚。

对于这道题而言，我们只能需要找到深度最高的那一层同时返回最左侧的值，所以需要用到回溯

```java
class Solution {

    int depth = 0;
    int maxDepth = Integer.MIN_VALUE;
    int leftMost = -1;

    public int findBottomLeftValue(TreeNode root) {
        dfs(root);
        return this.leftMost;
    }

    public void dfs(TreeNode root) {
        this.depth++;
        if (root == null) {
            return;
        }
       // 当一个节点是叶子节点并且是更新maxDepth的时候就说明是这一层最左侧的数值
        if (root.left == null && root.right == null && depth > maxDepth) {
            maxDepth = depth;
            this.leftMost = root.val;
        }
      
        dfs(root.left);
        this.depth--; // 回溯操作，让depth退回上一层的数值

        dfs(root.right);
        this.depth--;
    }
}
```

```java
class Solution {
    public int findBottomLeftValue(TreeNode root) {
        Queue<TreeNode> queue = new LinkedList<>();
        queue.add(root);
        int ans = 0;
        while (!queue.isEmpty()) {
            int size = queue.size();
            for(int i = 0; i < size; i++) {
                TreeNode curr = queue.poll();
              // i == 0就说明是这一层最左侧的数值
                if (i == 0) {
                    ans = curr.val;
                }
                if (curr.left != null) {
                    queue.add(curr.left);
                }
                if (curr.right != null) {
                    queue.add(curr.right);
                }
            }
        }
        return ans;
    }
}
```

