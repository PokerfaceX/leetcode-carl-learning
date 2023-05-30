### Question 216 Combination Sum III

![image-20230513170425800](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230513170425800.png)

这道题目和77题几乎是一模一样的写法，但是多了一个变量来记录当前的和

```java
class Solution {
    
    int currSum = 0;
    List<List<Integer>> ans = new ArrayList<>();
    List<Integer> path = new ArrayList<>();
    
    
    public List<List<Integer>> combinationSum3(int k, int n) {
        traversal(k, n, 1);
        return ans;
    }
    
    // 其实可以在这个方法的参数里面加入currSum那样的话就不用特意写上回溯的逻辑，因为计算机自动进行了回溯
    public void traversal(int k, int n, int start) {
      // 剪枝操作
        if (currSum >= n) {
            return;
        } 
      
        if (path.size() == k) {
            if (currSum == n) {
                ans.add(new ArrayList<>(path));
            }
            return;
        }
        //  这里也是一个剪枝的操作
        for(int i = start; i <= 9; i++) {
            currSum += i;
            path.add(i);
            traversal(k, n, i + 1);
            path.remove(path.size() - 1); // 回溯操作
            currSum -= i; // 回溯操作
        }
    }
}
```

k - path.size() 代表着我们还需要多少个数字，那么 9 减去这个数值再加上 1 就能告诉我们最多最多可以在哪里开始这个for循环

+1是因为我们要把for循环的起点包含在内