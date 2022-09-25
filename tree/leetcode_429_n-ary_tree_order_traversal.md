### Question 429 N-ary Tree Level Order Traversal

![image-20220922225635087](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220922225635087.png)

再次是一道经典的树层序遍历模板套用题目，只要稍微做一下调整就好

```java
class Solution {
    public List<List<Integer>> levelOrder(Node root) {
        Queue<Node> queue = new LinkedList<>();
        List<List<Integer>> ans = new ArrayList<>();
        if (root != null) {
            queue.add(root);
        }
        while (!queue.isEmpty()) {
            int size = queue.size();
            List<Integer> list = new ArrayList<>();
            while (size > 0) {
                Node curr = queue.poll();
                list.add(curr.val);
                // 用来加入每一个j
                for(Node tmp: curr.children) {
                    if (tmp != null) {
                         queue.add(tmp);
                    }
                }
                size--;
            }
            ans.add(list);
        }
        return ans;
    }
}
```

