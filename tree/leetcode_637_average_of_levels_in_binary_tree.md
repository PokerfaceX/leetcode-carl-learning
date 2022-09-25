### Question 637 Average of Levels in Binary Tree

![image-20220922221608564](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220922221608564.png)

又是在层序遍历的模板上进行一些小小的修改，只要在遍历当前层数的数值的时候，算出平均值就可以

~~~java
class Solution {
    public List<Double> averageOfLevels(TreeNode root) {
        List<Double> list = new ArrayList<>();
        Queue<TreeNode> queue = new LinkedList<>();
        if (root != null) {
            queue.add(root);
        }
        while (!queue.isEmpty()) {
            int size = queue.size();
            int i = size;
            double sum = 0;
            while (size > 0) {
                TreeNode curr = queue.poll();
                if (curr.left != null) {
                    queue.add(curr.left);
                }
                if (curr.right != null) {
                    queue.add(curr.right);
                }
                sum += curr.val;
                size--;
            }
            // size到最后是0，所以需要提前找一个变量来ji'l
            list.add(sum / i);
        }
        return list;
    }
}
~~~

