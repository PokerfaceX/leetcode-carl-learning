### Question 107 Binary Tree Level Order Traversal II

![image-20230505211600496](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230505211600496.png)

这道题目和leetcode 102题几乎是完全一样的，我们只需要在最后反转一下答案数组就可以了

```java
class Solution {
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        List<List<Integer>> ans = new ArrayList<>();
        Queue<TreeNode> queue = new LinkedList<>();
        if (root != null) {
            queue.add(root);
        }
        while (!queue.isEmpty()) {
            int size = queue.size();
            List<Integer> tmp = new ArrayList<>();
            while (size > 0) {
                TreeNode curr = queue.poll();
                tmp.add(curr.val);
                if (curr.left != null) {
                    queue.add(curr.left);
                }
                if (curr.right != null) {
                    queue.add(curr.right);
                }
                size--;
            }
            ans.add(tmp);
        }
        Collections.reverse(ans);
        return ans;
    }
}
```

