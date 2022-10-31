### Question 589 N-ary Tree Preorder Traversal

![image-20220927101415185](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220927101415185.png)

这道题目其实和普通的二叉树前序遍历几乎没有区别，只不过从左右子树变成了N叉树。

~~~java
class Solution {
    
    List<Integer> ans = new ArrayList<>();
    
    public List<Integer> preorder(Node root) {
        dfs(root);
        return ans;
    }
    
    public void dfs(Node root) {
        if (root == null) {
            return;
        }
        ans.add(root.val); // 中
        for(int i = 0; i < root.children.size(); i++) {
            dfs(root.children.get(i)); // lei'si
        }
    }
}
~~~

