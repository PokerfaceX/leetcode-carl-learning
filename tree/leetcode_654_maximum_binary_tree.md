### Question 654 Maximum Binary Tree

![image-20230508204239208](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230508204239208.png)

这道题目相对而言，比较简单，对于遍历顺序的话，一开始的时候没怎么想，但是慢慢研究就会发现，其实这种组建二叉树的题目肯定都是前序遍历，前面的leetcode_105和106都是类似的逻辑。



~~~java
class Solution {
    public TreeNode constructMaximumBinaryTree(int[] nums) {
        if (nums.length == 0) {
            return null;
        }   
        int biggest = Integer.MIN_VALUE;
        int index = -1;
        for(int i = 0; i < nums.length; i++) {
            if (nums[i] > biggest) {
                biggest = nums[i];
                index = i;
            }
        }
        int[] leftArray = Arrays.copyOfRange(nums, 0, index);
        int[] rightArray = Arrays.copyOfRange(nums, index + 1, nums.length);

        TreeNode currNode = new TreeNode(biggest);
        currNode.left = constructMaximumBinaryTree(leftArray);
        currNode.right = constructMaximumBinaryTree(rightArray);

        return currNode;
    }
}
~~~

上面的代码其实在时间复杂度和空间复杂度上会稍微冗余，因为Arrays.copyOfRange操作需要时常创建新的数组，非常消耗时间。

可以做一点优化

```java
class Solution {
    public TreeNode constructMaximumBinaryTree(int[] nums) {
        return construct(nums, 0, nums.length - 1);
    }
		// 这里我们一律用左闭右闭的选择
    public TreeNode construct(int[] nums, int start, int end) {
        if (end - start < 0) {
            return null;
        }
        int maxValue = Integer.MIN_VALUE;
        int index = -1;
        for(int i = start; i <= end; i++) {
            if (nums[i] > maxValue) {
                maxValue = nums[i];
                index = i;
            }
        }
        TreeNode currNode = new TreeNode(maxValue);
        currNode.left = construct(nums, start, index - 1);
        currNode.right = construct(nums, index + 1, end);
        return currNode;
    }
}
```

