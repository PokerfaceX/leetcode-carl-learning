### Question 590 N-ary Tree Postorder Traversal

![image-20220927102259746](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220927102259746.png)

这道题目和leetcode_589几乎是完全一样的，只是把顺序调换了下，另外稍微值得注意的点是处理的当前逻辑是应该放到for循环之后，否则会出现一点点bug

~~~java
class Solution {
    
    List<Integer> ans = new ArrayList<>();
    
    public List<Integer> postorder(Node root) {
        dfs(root);
        return ans;
    }
    
    public void dfs(Node root) {
        if (root == null) {
            return;
        }
        for(Node curr: root.children) {
            dfs(curr);
        }
        ans.add(root.val);
    }
}
~~~

