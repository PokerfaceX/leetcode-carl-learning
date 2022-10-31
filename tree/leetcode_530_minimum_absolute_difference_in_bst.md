### Question 530 Minimum Absolute Difference in BST

![image-20221025084549721](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20221025084549721.png)

这道题目其实一开始的想法再次错了，想着做一下的操作，但是其实这道题目的关键还是使用中序遍历，因为在中序遍历的时候，遍历的顺序是左中右，那么对于一个二叉搜索树而言，就可以完美的得到一个从小到大的数组

**错误想法**

```java
if (Maths.abs(root.val - root.left.val) < minDiff) minDiff = Maths.abs(root.val - root.left.val);

if (Maths.abs(root.val - root.right.val) < minDiff) minDiff = Maths.abs(root.val - root.right.val);
```

上代码

```java
class Solution {
    
    List<Integer> list = new ArrayList<>();
    
    public int getMinimumDifference(TreeNode root) {
        dfs(root);
        int diff = Integer.MAX_VALUE;
        for(int i = 0; i < list.size() - 1; i++) {
            if (Math.abs(list.get(i) - list.get(i + 1)) < diff) {
                diff = Math.abs(list.get(i) - list.get(i + 1));
            }
        }
        return diff;
    }
    
    public void dfs(TreeNode root) {
        if (root == null) {
            return;
        }
        dfs(root.left);
        list.add(root.val);
        dfs(root.right);
    }
}
```

以上的代码使用了额外的代码空间，那么就稍微优化一下，看看怎么样才能不使用额外的数组空间

```java
class Solution {
    
    int minDiff = Integer.MAX_VALUE;
    TreeNode prev = null; // 用来记录中序遍历时的前一个节点，用来做比较
    
    public int getMinimumDifference(TreeNode root) {
        dfs(root);
        return minDiff;
    }
    
    public void dfs(TreeNode root) {
        if (root == null) {
            return;
        }
        // 遍历左子树
        dfs(root.left);
        // 遍历完左子树之后，中的，处理逻辑
        if (prev != null && Math.abs(prev.val - root.val) < minDiff) {
            minDiff = Math.abs(prev.val - root.val);
        }
        prev = root;
        // 遍历
        dfs(root.right);
    }
}
```

