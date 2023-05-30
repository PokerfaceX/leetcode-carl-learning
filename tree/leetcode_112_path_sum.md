### Question 112 Path Sum

![image-20230507162839042](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230507162839042.png)

这道题目又是一道经典的回溯算法，代码逻辑本身不难，我的想法就是加上当前的数值，然后向下遍历，往上返回的时候进行回溯，但是错就错在了扣除叶子节点的数值的时候，什么时候应该回溯，什么时候应该返回，弄错了

```java
class Solution {

    private boolean hasPath;
    private int currSum = 0;

    public boolean hasPathSum(TreeNode root, int targetSum) {
        dfs(root, targetSum);
        return this.hasPath;
    }

    public void dfs(TreeNode root, int targetSum) {
      // 空节点就直接跳过  
      if (root == null) {
            return;
        }
      // 直接添加当前节点的数值
        this.currSum += root.val;
      // 我们必须得看当前是不是一个叶子节点并且currSum == targetSum
        if (currSum == targetSum && root.left == null && root.right == null) {
            this.hasPath = true;
        }
        dfs(root.left, targetSum);
        dfs(root.right, targetSum); // 这里想像成我们已经检查了左右子树，当全部完成之后在回溯
        this.currSum -= root.val; // 回溯操作，既然添加了一次，那么回溯肯定也是一次
    }
}
```

