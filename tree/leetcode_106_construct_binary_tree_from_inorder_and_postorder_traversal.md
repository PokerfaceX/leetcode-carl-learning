### Question 106 Construct Binary Tree from Inorder and Postorder Traversal

![image-20221001205543507](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20221001205543507.png)

其实这道题目，卡哥网站的讲解非常的好，这里简单说下就是，题目里给了中序遍历(左中右)和后序遍历的数组(左右中)。显而易见，我们其实是需要使用递归的，因为涉及到数组的不断分割以及多层返回。那么从上面的第一个例子里其实就可以看出，postorder数组里面最后的元素，肯定是中间节点，也就是当前子树的根节点。那么找到这个节点，在找到在中序数组这个根节点的位置，就能知道当前子树的左子树包含多少个节点，右子树包含了几个节点。具体的逻辑的话，看下图

![image-20221001210004691](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20221001210004691.png)

直接上代码解释

```java
class Solution {
    public TreeNode buildTree(int[] inorder, int[] postorder) {
        // 如果两个数组任意一个长度为零就说明是个null节点
        if (postorder.length == 0) {
            return null;
        }
        TreeNode root = new TreeNode(postorder[postorder.length - 1]);
        int middleIndex = 0;
        for(; middleIndex < inorder.length; middleIndex++) {
            if (inorder[middleIndex] == root.val) {
                break;
            }
        }
        // 对于一切子数组，一切使用左闭右开的原则
        // copyOfRange返回的子数组从start(inclusive)到end(ex)
        int[] leftInorder = Arrays.copyOfRange(inorder, 0, middleIndex);
        int[] rightInorder = Arrays.copyOfRange(inorder, middleIndex + 1, inorder.length);
        int[] leftPostOrder = Arrays.copyOfRange(postorder, 0, leftInorder.length);
        int[] rightPostOrder = Arrays.copyOfRange(postorder, leftInorder.length, postorder.length - 1);
        
        root.left = buildTree(leftInorder, leftPostOrder);
        root.right = buildTree(rightInorder, rightPostOrder);
        
        return root;
    }
}
```

