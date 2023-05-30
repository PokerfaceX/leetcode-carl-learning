### Question 105 Construct Binary Tree From Preorder and Inorder Traversal

![image-20230508203218101](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230508203218101.png)

这道题目和leetcode_106题完全是一个思路，只要理解了leetcode_106题，那么就完全没问题。这里的话，为了方便理解，放一个链接

https://nicksxs.me/2020/12/13/Leetcode-105-%E4%BB%8E%E5%89%8D%E5%BA%8F%E4%B8%8E%E4%B8%AD%E5%BA%8F%E9%81%8D%E5%8E%86%E5%BA%8F%E5%88%97%E6%9E%84%E9%80%A0%E4%BA%8C%E5%8F%89%E6%A0%91-Construct-Binary-Tree-from-Preorder-and-Inorder-Traversal-%E9%A2%98%E8%A7%A3%E5%88%86%E6%9E%90/



```java
class Solution {
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        if (preorder.length == 0) {
            return null;
        }
        int rootValue = preorder[0];
        int index = -1;
        for(int i = 0; i < inorder.length; i++) {
            if (inorder[i] == rootValue) {
                index = i;
                break;
            }
        }

        int[] leftInorder = Arrays.copyOfRange(inorder, 0, index);
        int[] rightInorder = Arrays.copyOfRange(inorder, index + 1, inorder.length);

        int[] leftPreorder = Arrays.copyOfRange(preorder, 1, 1 + leftInorder.length);
        int[] rightPreorder = Arrays.copyOfRange(preorder, 1 + leftInorder.length, preorder.length);

        TreeNode currNode = new TreeNode(rootValue);
        currNode.left = buildTree(leftPreorder, leftInorder);
        currNode.right = buildTree(rightPreorder, rightInorder);

        return currNode;
    }
}
```

