### Question 46 Permutations

![image-20221125202247911](/Users/jasonjin/Library/Application Support/typora-user-images/image-20221125202247911.png)

这道题目其实也是一道回溯算法的经典利用，和前面的题目最大的不同便是移除了startIndex的存在并且每一次树层遍历都需要从i == 0开始



![image-20221125202434824](/Users/jasonjin/Library/Application Support/typora-user-images/image-20221125202434824.png)

可以看到其实我们需要一个used数组来来确保每一个数字都是只使用了一次



```java
class Solution {

    boolean[] used; // 需要用一个used数组来记载什么数值已经被使用过了，比如找[1,2,3]和[1,3,2]的时候，需要知道对于当前遍历而言，哪些数字已经被用过了，所以应该在for循环里被跳过
    List<Integer> path = new ArrayList<>();
    List<List<Integer>> ans = new ArrayList<>();

    public List<List<Integer>> permute(int[] nums) {
        this.used = new boolean[nums.length];
        backtracking(nums);
        return this.ans;
    }

    public void backtracking(int[] nums) {
        if (path.size() == nums.length) {
            ans.add(new ArrayList<>(path));
            return;
        }
        for(int i = 0; i < nums.length; i++) {
            if (used[i]) {
                continue;
            }
            path.add(nums[i]);
            used[i] = true;
            backtracking(nums);
            used[i] = false;
            path.remove(path.size() - 1);
        }
    }
}
```

