### Question 637 Average of Levels in Binary Tree

![image-20230505213137028](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230505213137028.png)

又是在层序遍历的模板上进行一些小小的修改，只要在遍历当前层数的数值的时候，算出平均值就可以

~~~java
class Solution {
    public List<Double> averageOfLevels(TreeNode root) {
        List<Double> ans = new ArrayList<>();
        if (root == null) {
            return ans;
        }
        Queue<TreeNode> queue = new LinkedList<>();
        queue.add(root);
        while (!queue.isEmpty()) {
            int size = queue.size();
            Double sum = 0.0;
            for(int i = 0; i < size; i++) {
                TreeNode curr = queue.poll();
                if (curr.left != null) {
                    queue.add(curr.left);
                }
                if (curr.right != null) {
                    queue.add(curr.right);
                }
                sum += curr.val;
            }
            ans.add(sum / size);
        }
        return ans;
    }
}
~~~

