### Question 429 N-ary Tree Level Order Traversal

![image-20230505214015302](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230505214015302.png)

再次是一道经典的树层序遍历模板套用题目，只要稍微做一下调整就好

```java
class Solution {
    public List<List<Integer>> levelOrder(Node root) {
        List<List<Integer>> ans = new ArrayList<>();
        if (root == null) {
            return ans;
        }
        Queue<Node> queue = new LinkedList<>();
        queue.add(root);
        while (!queue.isEmpty()) {
            int size = queue.size();
            List<Integer> currLayer = new ArrayList<>();
            for(int i = 0; i < size; i++) {
                Node curr = queue.poll();
                for(Node tmp: curr.children) {
                    if (tmp != null) {
                        queue.add(tmp);
                    }
                }
                currLayer.add(curr.val);
            }
            ans.add(currLayer);
        }
        return ans;
    }
}
```

