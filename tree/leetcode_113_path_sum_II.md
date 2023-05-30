### Question 113 Path Sum II

![image-20230507164107620](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230507164107620.png)

和112题是一摸一样的套路，只不过是多了一个path来记录当前的路径

```java
class Solution {

    List<Integer> path = new ArrayList<>();
    List<List<Integer>> ans = new ArrayList<>();
    int currSum = 0; // 这里需要一个currSum，要不然每次找到叶子节点的时候，就要重新算一次路径之和

    public List<List<Integer>> pathSum(TreeNode root, int targetSum) {
        dfs(root, targetSum);
        return ans;
    }

    public void dfs(TreeNode root, int targetSum) {
        if (root == null) {
            return;
        }
        currSum += root.val;
        path.add(root.val);
        if (root.left == null && root.right == null && currSum == targetSum) {
            ans.add(new ArrayList<>(path));
        }
        dfs(root.left, targetSum);
        dfs(root.right, targetSum);
      // 回溯操作，跟112比多了一个需要维护的path
        path.remove(path.size() - 1);
        currSum -= root.val;
    }
}
```

