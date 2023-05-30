### Question 236 Lowest Common Ancestor of a Binary Tree

![image-20230509133718690](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230509133718690.png)

![image-20230509133731662](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230509133731662.png)

这道题目一开始的时候是蒙蔽的，因为直观的来看，我们需要从底部来往上看，所以得是用到后续遍历（左右中） 我们需要从左子树和右子树返回东西之后做判断。其实这道题目的核心思想就是，因为后续遍历的顺序是**左右中**，那么我们就看左子树和右子树返回的东西有啥，如果都不是空，就说明是节点的祖先，如果只有一个子树包含了p或者q，那么也要返回，因为就说明当前节点是至少一个节点的祖先

```java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (root == null) {
            return null;
        }    
        if (root == p || root == q) {
            return root;
        }
        TreeNode leftFound = lowestCommonAncestor(root.left, p, q);
        TreeNode rightFound = lowestCommonAncestor(root.right, p, q);
      	// 如果左侧和右侧都不是null，那就说明左右分别包含了p或者q，所以当前节点就是公公祖先
        if (leftFound != null && rightFound != null) {
            return root;
        } else if (leftFound != null && rightFound == null) {
            return leftFound;
        } else if (leftFound == null && rightFound != null) {
            return rightFound;
        } else {
            return null;
        }
    }
}
```

其实我一开始的时候，也没有完全理解，尤其是example2，根本不太清楚，但是仔细看了卡哥的视频就发现，example2的情况其实在我们的代码里已经覆盖了，当我们找到一个p或者q的时候就可以直接返回，我们的代码可以处理这种情况

![image-20230509134052490](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230509134052490.png)

卡哥视频讲解的很好： https://www.bilibili.com/video/BV1jd4y1B7E2/?spm_id_from=333.788&vd_source=60e6f0aa6d18b1e267c1a770a39b7276