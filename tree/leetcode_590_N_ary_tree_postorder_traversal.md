### Question 590 N-ary Tree Postorder Traversal

![image-20230506193038725](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230506193038725.png)

这道题目和leetcode_589几乎是完全一样的，只是把顺序调换了下，另外稍微值得注意的点是处理的当前逻辑是应该放到for循环之后，因为这里是后续遍历，对于一个递归函数而言，定义如何调用自身非常重要，这里的话我们先相信我们在所有子节点完成了工作之后，再加上当前节点的数值就行

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

