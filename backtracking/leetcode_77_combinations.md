### Question 77 Combinations

![image-20221103141624555](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20221103141624555.png)

这道题目算是一个经典的回溯算法的应用了，直接上代码解释

```java
class Solution {
    
    List<List<Integer>> ans = new ArrayList<>();
    List<Integer> path = new ArrayList<>();
    
    public List<List<Integer>> combine(int n, int k) {
        backtracking(n, 1, k);
        return ans;
    }
    
    public void backtracking(int n, int start, int k) {
        if (path.size() == k) {
            ans.add(new ArrayList<>(path)); //cun'f'gang
            return;
        }
        for(int i = start; i <= n; i++) {
            path.add(i); // 处理节点
            backtracking(n , i + 1, k); // 递归
            path.remove(path.size() - 1); // 回溯，撤销处理结果
        }
    }
    
    // 剪枝操作
    for(int i = start; i <= n - (k - path.size()) + 1; i++) {
            path.add(i);
            backtracking(n , i + 1, k);
            path.remove(path.size() - 1);
        }
}
```

![image-20221103145000219](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20221103145000219.png)
