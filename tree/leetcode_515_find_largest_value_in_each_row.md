### Question 515 Find Largest Value in Each Tree Row

![image-20220923202959620](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220923202959620.png)

这道题目只需要套用层序遍历的模板就好，我们通过queue来进行bfs遍历，只不过在每一层找到最大的值

```java
class Solution {
    public List<Integer> largestValues(TreeNode root) {
        List<Integer> ans = new ArrayList<>();
        Queue<TreeNode> queue = new LinkedList<>();
        if (root != null) {
            queue.add(root);
        }
        while (!queue.isEmpty()) {
            int size = queue.size();
            int max = Integer.MIN_VALUE;
            while (size > 0) {
                TreeNode curr = queue.poll();
                if (curr.val > max) {
                    max = curr.val;
                }
                if (curr.left != null) {
                    queue.add(curr.left);                    
                }
                if (curr.right != null) {
                    queue.add(curr.right);
                }
                size--;
            }
            ans.add(max);
        }
        return ans;
    }
}
```

