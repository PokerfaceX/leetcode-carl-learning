### Question 257 Binary Tree Paths

![image-20230507151535842](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230507151535842.png)

这道题目问的是从根节点到所有叶子节点的path，那么很显然我们需要使用前序遍历，因为我们要先处理当前节点再去处理左子树和右子树。但是有一点需要注意，那就是这道题目需要使用到回溯算法，因为我们遍历到叶子节点之后还需要逐渐把节点从当前路径中删除，以此来找到新的路径。

```java
class Solution {

    List<String> ans = new ArrayList<>();
    List<String> path = new ArrayList<>();

    public List<String> binaryTreePaths(TreeNode root) {
        dfs(root);
        return ans;
    }

    public void dfs(TreeNode root) {
       // 直接加入当前节点的值，通过下面的两个if语句我们可以避开所有root==null的情况，并且这道题目里也说了node的最小数量为1，所以root永远不会是null
        path.add(String.valueOf(root.val));
        if (root.left == null && root.right == null) {
            StringBuffer sb = new StringBuffer();
            for(int i = 0; i < path.size() - 1; i++) {
                sb.append(path.get(i) + "->");
            }
            sb.append(path.get(path.size() - 1));
            ans.add(sb.toString());
        }
        if (root.left != null) {
            dfs(root.left);
          	// 回溯
            path.remove(path.size() - 1);
        }
        if (root.right != null) {
            dfs(root.right);
          	// 回溯
            path.remove(path.size() - 1);
        }
    }
}
```

上面的话我们回溯的过程标记的非常清楚，其实可以使用精简代码来隐藏

```java
class Solution {
    
    public List<String> binaryTreePaths(TreeNode root) {
        List<String> result = new ArrayList<>();
        List<Integer> path = new ArrayList<>();
        dfs(root, result, "");
        return result;
    }
    
    // 这里的string s其实就能代表回溯的过程，因为是值赋值而不是地址赋值，每次传入栈的东西都是不同的，而回退的时候就会自动回退到当时的状态
    public void dfs(TreeNode root, List<String> result, String s) {
        s += root.val;
        if (root.left == null && root.right == null) { 
            result.add(s);
            return;
        }
        if (root.left != null) {
            dfs(root.left, result, s + "->");
        }
        if (root.right != null) {
            dfs(root.right, result, s + "->");
        } 
        
    }
}
```

