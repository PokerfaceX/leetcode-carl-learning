### Question 105 Construct Binary Tree From Preorder and Inorder Traversal

![image-20221001215638470](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20221001215638470.png)

这道题目和leetcode_106题完全是一个思路，只要理解了leetcode_106题，那么就完全没问题。这里的话，为了方便理解，放一个链接

https://nicksxs.me/2020/12/13/Leetcode-105-%E4%BB%8E%E5%89%8D%E5%BA%8F%E4%B8%8E%E4%B8%AD%E5%BA%8F%E9%81%8D%E5%8E%86%E5%BA%8F%E5%88%97%E6%9E%84%E9%80%A0%E4%BA%8C%E5%8F%89%E6%A0%91-Construct-Binary-Tree-from-Preorder-and-Inorder-Traversal-%E9%A2%98%E8%A7%A3%E5%88%86%E6%9E%90/



```java
class Solution {
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        if (preorder.length == 0) {
            return null;
        }
        TreeNode currRoot = new TreeNode(preorder[0]);
        int middleIndex = 0;
        for(; middleIndex < inorder.length; middleIndex++) {
            if (inorder[middleIndex] == currRoot.val) {
                break;
            }
        }
        
        int[] leftIn = Arrays.copyOfRange(inorder, 0, middleIndex);
        int[] rightIn = Arrays.copyOfRange(inorder, middleIndex + 1, inorder.length);
        
        int[] leftPre = Arrays.copyOfRange(preorder, 1, 1 + middleIndex);
        int[] rightPre = Arrays.copyOfRange(preorder, 1 + middleIndex, preorder.length);
        
        // 下面的话两个变量的顺序放错了ji
        currRoot.left = buildTree(leftPre, leftIn);
        currRoot.right = buildTree(rightPre, rightIn);
        return currRoot;
    }
}
```

