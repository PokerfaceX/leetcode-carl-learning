### Question 530 Minimum Absolute Difference in BST

![image-20230508212025331](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230508212025331.png)

![image-20230508212018143](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230508212018143.png)

这道题目其实一开始的想法再次错了，我还是想着只要每次比较中间节点和他的左右孩子就行了，但是实际上是，在上面的例子中，最小的diff其实是9，如果我只比较中间节点和左右孩子，那么上面的例子就只能给我123



上代码

```java
class Solution {

    List<Integer> list = new LinkedList<>();

    public int getMinimumDifference(TreeNode root) {
        dfs(root);
        int smallestDiff = Integer.MAX_VALUE;
        for(int i = 0; i < list.size() - 1; i++) {
            int diff = Math.abs(list.get(i) - list.get(i + 1));
            if (diff < smallestDiff) {
                smallestDiff = diff;
            }
        }
        return smallestDiff;
    }

    public void dfs(TreeNode root) {
        if (root == null) {
            return;
        }
        dfs(root.left);
        this.list.add(root.val);
        dfs(root.right);
    }
}
```

以上的代码使用了额外的代码空间，那么就稍微优化一下，看看怎么样才能不使用额外的数组空间，这里的双指针法中，curr指针是自动回溯的，因为他是传到了一个方法当成了一个参数，我们不用手动回溯，他自己就会完成

```java
class Solution {
		
  // 双指针遍历，这个指针永远指向curr前面的一个节点
    TreeNode prev = null;
    int diff = Integer.MAX_VALUE;

    public int getMinimumDifference(TreeNode root) {
        dfs(root);
        return diff;
    }

    public void dfs(TreeNode root) {
        if (root == null) {
            return;
        }
        dfs(root.left);
        if (prev != null) {
            diff = Math.min(diff, Math.abs(root.val - prev.val));
        }
      // prev跟上null
        prev = root;
        dfs(root.right);
    }
}
```

