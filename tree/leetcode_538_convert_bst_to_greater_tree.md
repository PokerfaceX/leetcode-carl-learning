### Question 538 Convert BST to Greater Tree

![image-20221101095826021](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20221101095826021.png)

这道题目一开始想的时候没什么头绪，但是看了下提示发现，其实就是使用右中左的遍历方式，才逐渐递增每个数值的节点。类似于把一个数组比如[1,2,3,4,5]变成[15,14,12,9,5]的过程，只不过是变成了二叉树

~~~java
class Solution {
    
    int prev = 0; // 用来记录上一个数值，因为是逐渐累加的，需要一个变量来记录上一个累计的最大值，这里可以用TreeNode来代替但是还得处理空指针的情况，不是很方便
    
    public TreeNode convertBST(TreeNode root) {
        traversal(root);
        return root;
    }
    
    public void traversal(TreeNode curr) {
        if (curr == null) {
            return;
        }
        // 右
        traversal(curr.right);
        // 中
        curr.val = curr.val + prev;
        prev = curr.val;
        // 左
        traversal(curr.left);
        
    }
}
~~~

