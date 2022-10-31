### Question 257 Binary Tree Paths

![image-20220926121849894](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220926121849894.png)

这道题目问的是从根节点到所有叶子节点的path，那么很显然我们需要使用前序遍历，因为我们要先处理当前节点再去处理左子树和右子树。但是有一点需要注意，那就是这道题目需要使用到回溯算法，因为我们遍历到叶子节点之后还需要逐渐把节点从当前路径中删除，以此来找到新的路径。

```java
class Solution {
    
    public List<String> binaryTreePaths(TreeNode root) {
        List<String> result = new ArrayList<>();
        List<Integer> path = new ArrayList<>();
        dfs(root, result, path);
        return result;
    }
    
    public void dfs(TreeNode root, List<String> result, List<Integer> path) {
        // 这道题目规定节点数量最少是1，所以不用担心一开始root为空，其次就是我们在底下会处理空的情况
        // 中, 加入节点到路径
        path.add(root.val);
        if (root.left == null && root.right == null) {
            // 找到叶子节点的话就把路径加到result数组中
            StringBuffer s = new StringBuffer();
            for(int i = 0; i < path.size() - 1; i++) {
                s.append(String.valueOf(path.get(i)) + "->");
            }
            s.append(String.valueOf(path.get(path.size() - 1)));
            result.add(s.toString());
            return;
        }
        // 这样可以有效防止出现空指针访问，其实就是在回溯的时候，保证弹出的都是应该弹出的路径最后一个节点
        if (root.left != null) {
            dfs(root.left, result, path);
            path.remove(path.size() - 1);
        }
        if (root.right != null) {
             dfs(root.right, result, path);
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

