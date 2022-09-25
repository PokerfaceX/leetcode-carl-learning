### Question 199 Binary Tree Right Side View

![image-20220922220447384](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220922220447384.png)

这道题目还是套用层序遍历的模板的，只需要在pop当前层的元素的时候，把最后一个元素加进去就好了

```java
class Solution {
    public List<Integer> rightSideView(TreeNode root) {
        List<Integer> ans = new ArrayList<>();
        Queue<TreeNode> queue = new LinkedList<>();
        if (root != null) {
            queue.add(root);
        }
        while (!queue.isEmpty()) {
            int size = queue.size();
            while (size > 0) {
                TreeNode curr = queue.poll();
                if (curr.left != null) {
                    queue.add(curr.left);
                }
                if (curr.right != null) {
                    queue.add(curr.right);
                }
                if (size == 1) {
                    ans.add(curr.val);
                }
                size--;
            }
        }
        return ans;
    }
}
```

