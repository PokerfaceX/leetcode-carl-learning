### Question 404 Sum Of Left Leaves

![image-20220926125736009](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220926125736009.png)

这道题目的话，刚开始我想的就是直接进行前序遍历，对于当前节点直接判断他的左孩子是不是左侧叶子节点，如果是的话直接返回左孩子数值否则继续进行遍历。
~~~java
class Solution {
    
    int sum = 0;
    
    public int sumOfLeftLeaves(TreeNode root) {
        getLeftLeafSum(root);
        return sum;
    }
    
    public void getLeftLeafSum(TreeNode root) {
        if (root == null) {
            return;
        }
        if (root.left != null && root.left.left == null && root.left.right == null) {
            sum += root.left.val;
        }
        getLeftLeafSum(root.left);
        getLeftLeafSum(root.right);
    }
}
~~~

但是写完了之后其实不太满意，感觉有点冗余而且也感觉前序遍历不是那么恰当，所以看了下卡哥的代码。发现其实还是还是用后续遍历，代码会简洁很多，也蛮好理解的

```java
class Solution {
    
    
    public int sumOfLeftLeaves(TreeNode root) {
        if (root == null) {
            return 0;
        }
        int leftLeafValue = sumOfLeftLeaves(root.left); // 左
        // 左侧遍历的时候万一碰到了左测叶子节点，那么处理它
        if (root.left != null && root.left.left == null && root.left.right == null) {
            leftLeafValue = root.left.val; // 一开始写了return，但是那样的话永远无法遍历右子树，所以是错的
        }
        int rightLeftLeafValue = sumOfLeftLeaves(root.right); // 右
        
        int total = leftLeafValue + rightLeftLeafValue; // 中
        return total;
    }
    
    
}
```

