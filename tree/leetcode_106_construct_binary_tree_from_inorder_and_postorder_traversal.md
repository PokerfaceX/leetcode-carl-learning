### Question 106 Construct Binary Tree from Inorder and Postorder Traversal

![image-20230508201520233](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230508201520233.png)

其实这道题目，卡哥网站的讲解非常的好，这里简单说下就是，题目里给了中序遍历(左中右)和后序遍历的数组(左右中)。显而易见，我们其实是需要使用递归的，因为涉及到数组的不断分割以及多层返回。那么从上面的第一个例子里其实就可以看出，postorder数组里面最后的元素，肯定是中间节点，也就是当前子树的根节点。那么找到这个节点，在找到在中序数组这个根节点的位置，就能知道当前子树的左子树包含多少个节点，右子树包含了几个节点。具体的逻辑的话，看下图

![image-20230508201345473](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230508201345473.png)

直接上代码解释

```java
class Solution {
    public TreeNode buildTree(int[] inorder, int[] postorder) {
      // 这里inorder或者postorder为0都可以  
      if (inorder.length == 0) {
            return null;
        }
      // 在后续遍历数组的最后一个数值就是我们当前递归这一层想要的root节点
        int rootValue = postorder[postorder.length - 1];
        int index = -1;
      // 找到中序遍历中的root节点，那样我们就知道左子树和右子树的范围，从而确定前序遍历和后续遍历的数组
        for(int i = 0; i < inorder.length; i++) {
            if (inorder[i] == rootValue) {
                index = i;
                break;
            }
        }
      // 这里一贯使用左闭右闭的原则，所以传进去的数组永远都是我们想看到的值，而不会包含没用的数值
        int[] leftInorder = Arrays.copyOfRange(inorder, 0, index);
        int[] rightInorder = Arrays.copyOfRange(inorder, index + 1, inorder.length);

        int[] leftPostorder = Arrays.copyOfRange(postorder, 0, leftInorder.length);
        int[] rightPostorder = Arrays.copyOfRange(postorder, leftInorder.length, postorder.length - 1);

        TreeNode currNode = new TreeNode(rootValue);
        currNode.left = buildTree(leftInorder, leftPostorder);
        currNode.right = buildTree(rightInorder, rightPostorder);
				
       // 我们每次都会返回当前这一层的“root”节点，从而完成递归
        return currNode;


    }
}
```

