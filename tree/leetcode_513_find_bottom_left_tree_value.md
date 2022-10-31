### Question 513 Find Bottom Left Tree Value

![image-20220927100537286](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220927100537286.png)

做任何一道题目之前，都要保证我们完全理解了题目，这道题问的是最后一行的最左值，而不是单单整个树里面最左侧的值，这一点要搞清楚。

对于这道题而言，我们只能需要找到深度最高的那一层同时返回最左侧的值，所以需要用到回溯

```java
class Solution {
    
    int maxDepth = Integer.MIN_VALUE;
    int currDepth = 0;
    int result;
    
    public int findBottomLeftValue(TreeNode root) {
        dfs(root);
        return result;
    }
    
    public void dfs(TreeNode root) {
        currDepth++;
        // 下面避免了root为空的情况，只需要做depth的判断和叶子节点的判断就好
        if (root.left == null && root.right == null) {
            if (currDepth > maxDepth) {
                maxDepth = currDepth;
                result = root.val;
            }
        }
        if (root.left != null) {
            dfs(root.left);
            currDepth--; // 回溯要不然depth在遍历第二层的右子树的时候就是3了
        }
        if (root.right != null) {
            dfs(root.right);
            currDepth--;
        }
    }
}
```

