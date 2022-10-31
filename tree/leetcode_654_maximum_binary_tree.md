### Question 654 Maximum Binary Tree

![image-20221022210434731](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20221022210434731.png)

![image-20221022210453566](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20221022210453566.png)

这道题目相对而言，比较简单，对于遍历顺序的话，一开始的时候没怎么想，但是慢慢研究就会发现，其实这种组建二叉树的题目肯定都是前序遍历，前面的leetcode_105和106都是类似的逻辑。



~~~java
class Solution {
    public TreeNode constructMaximumBinaryTree(int[] nums) {
        if (nums.length == 0) {
            return null;
        }
        int maxValue = -1;
        int index = -1;
        // 前序遍历里面用于处理当前节点的逻辑
        for(int i = 0; i < nums.length; i++) {
            if (nums[i] > maxValue) {
                index = i;
                maxValue = nums[i];
            }
        }
        // 当前节点就是目前数组里最大的数值
        TreeNode curr = new TreeNode(maxValue);
        // 左子树，左闭右开
        curr.left = constructMaximumBinaryTree(Arrays.copyOfRange(nums, 0, index));
        // 右子树，左闭右开
        curr.right = constructMaximumBinaryTree(Arrays.copyOfRange(nums, index + 1, nums.length));
        
        return curr; // 最后需要将根节点返还回去，同时每一层递归都返还了当前构造的节点，二叉树才能被chuang'ji
    }
    
    
}
~~~

上面的代码其实在时间复杂度和空间复杂度上会稍微冗余，因为Arrays.copyOfRange操作需要时常创建新的数组，非常消耗时间。

可以做一点优化

```java
class Solution {
    public TreeNode constructMaximumBinaryTree(int[] nums) {
        
        return constructTree(nums, 0, nums.length);
    }
    // 和上面的逻辑几乎是完全一样的
    public TreeNode constructTree(int[] nums, int start, int finish) {
        // 当start >= finish的时候，说明这个数组为空，因为我们采用左闭右开原则
        if (start >= finish) {
            return null;
        }
        int maxValue = -1;
        int index = -1;
        // i从start开始
        for(int i = start; i < finish; i++) {
            if (nums[i] > maxValue) {
                index = i;
                maxValue = nums[i];
            }
        }
        // 下面同样的中左右
        TreeNode curr = new TreeNode(maxValue);
        curr.left = constructTree(nums, start, index);
        curr.right = constructTree(nums, index + 1, finish);
        return curr;
    }
}
```

