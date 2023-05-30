### Question 199 Binary Tree Right Side View

![image-20230505212714221](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230505212714221.png)

这道题目还是套用层序遍历的模板的，只需要在pop当前层的元素的时候，把最后一个元素加进去就好了

```java
class Solution {
    public List<Integer> rightSideView(TreeNode root) {
        List<Integer> ans = new ArrayList<>();
        if (root == null) {
            return ans;
        }
        Queue<TreeNode> queue = new LinkedList<>();
        queue.add(root);
        while (!queue.isEmpty()) {
            int size = queue.size();
            for(int i = 0; i < size; i++) {
                TreeNode curr = queue.poll();
                if (curr.left != null) {
                    queue.add(curr.left);
                } 
                if (curr.right != null) {
                    queue.add(curr.right);
                }
                if (i == size - 1) {
                    ans.add(curr.val);
                }
            }
        }
        return ans;
    }
}
```

