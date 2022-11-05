### Question 39 Combination Sum

![image-20221105220902829](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20221105220902829.png)

这道题目也是一道经典的回溯遍历的问题，但是唯一的不同就是说在递归的时候可以遍历重复的数字

![image-20221105221938189](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20221105221938189.png)



```java
class Solution {
    
    List<Integer> path = new ArrayList<>();
    List<List<Integer>> ans = new ArrayList<>();
    int currSum = 0;
    
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        Arrays.sort(candidates);
        traversal(candidates, 0, target);
        return ans;
    }

    public void traversal(int[] candidates, int currIndex, int target) {
        if (currSum == target) {
            ans.add(new ArrayList<>(path));
            return;
        }
        if (currSum > target) {
            return;
        }
        for(int i = currIndex; i < candidates.length; i++) {
            if (currSum + candidates[i] > target) break; // 这里就是最关键的一个剪枝操作，可以在上面途中看到虽然和为7和5的时候都会return但是还是会生成这两个无用的树枝，通过这个就可以在生成树枝之前就jian'duan
            currSum += candidates[i];
            path.add(candidates[i]);
            traversal(candidates, i, target); // 这里就是最重要的，一开始把这里的i写成了currIndex不断地报错
            path.remove(path.size() - 1);
            currSum -= candidates[i];
        }
    }
}
```

