### Question 108 Convert Sorted Array to Binary Search Tree

![image-20230510222755541](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230510222755541.png)

对于这道题目，一开始的时候想复杂了，但是一看到卡哥的代码就有了思路只要不断的找中间节点，然后一边分割数组，一边构造二叉树就行，算是一个中序遍历



~~~java
class Solution {
    public TreeNode sortedArrayToBST(int[] nums) {
        return traversal(nums, 0, nums.length - 1);
    }
    
    public TreeNode traversal(int[] nums, int left, int right) {
        // 这里采用左闭右闭的做法，所以left == right是valid的，也就是数组长度为1的情况，只有超过才是invalid
        if (left > right) {
            return null;
        }
        int mid = (left + right) / 2;
        TreeNode curr = new TreeNode(nums[mid]);
        curr.left = traversal(nums, left, mid - 1);
        curr.right = traversal(nums, mid + 1, right);
        return curr;
    }
}
~~~

