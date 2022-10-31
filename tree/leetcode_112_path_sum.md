### Question 112 Path Sum

![image-20220929223030041](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220929223030041.png)

这道题目又是一道经典的回溯算法，代码逻辑本身不难，我的想法就是加上当前的数值，然后向下遍历，往上返回的时候进行回溯，但是错就错在了扣除叶子节点的数值的时候，什么时候应该回溯，什么时候应该返回，弄错了

```java
class Solution {
    
   
    boolean found = false;
    int currSum = 0;
    
    public boolean hasPathSum(TreeNode root, int targetSum) {
        if (root == null) {
            return false;
        }
        dfs(root, targetSum);
        return found;
    }
    
    public void dfs(TreeNode root, int target) {       
        currSum += root.val; // 加入当前节点的值
        if (root.left == null && root.right == null) {
            if (currSum == target) found = true;
        }
        if (root.left != null) {
            dfs(root.left, target);
            // 若是把回溯的减法放在这里，就无法处理叶子节点的数值扣除
        }
        if (found) return; // jian'zhi'cao'zuo
        if (root.right != null) {
            dfs(root.right, target);
        }
        currSum -= root.val; // 这里就是回溯的关键，不能放在别的地方
    }
}
```

