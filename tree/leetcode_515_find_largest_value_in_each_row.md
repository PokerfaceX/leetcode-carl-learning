### Question 515 Find Largest Value in Each Tree Row

![image-20230505214500994](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230505214500994.png)

这道题目只需要套用层序遍历的模板就好，我们通过queue来进行bfs遍历，只不过在每一层找到最大的值

```java
class Solution {
    public List<Integer> largestValues(TreeNode root) {
        List<Integer> ans = new ArrayList<>();
        if (root == null) {
            return ans;
        }
        Queue<TreeNode> queue = new LinkedList<>();
        queue.add(root);
        while (!queue.isEmpty()) {
            int size = queue.size();
            Integer largest = Integer.MIN_VALUE;
            for(int i = 0; i < size; i++) {
                TreeNode curr = queue.poll();
                if (curr.left != null) {
                    queue.add(curr.left);
                }
                if (curr.right != null) {
                    queue.add(curr.right);
                }
                if (curr.val > largest) {
                    largest = curr.val;
                }
            }
            ans.add(largest);
        }
        return ans;
    }
}
```

