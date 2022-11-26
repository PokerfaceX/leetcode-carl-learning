### Question 46 Permutations

![image-20221125202247911](/Users/jasonjin/Library/Application Support/typora-user-images/image-20221125202247911.png)

这道题目其实也是一道回溯算法的经典利用，和前面的题目最大的不同便是移除了startIndex的存在并且每一次树层遍历都需要从i == 0开始



![image-20221125202434824](/Users/jasonjin/Library/Application Support/typora-user-images/image-20221125202434824.png)

可以看到其实我们需要一个used数组来来确保每一个数字都是只使用了一次



```java
class Solution {
    
    List<Integer> path = new ArrayList<>();
    List<List<Integer>> ans = new ArrayList<>();
    boolean[] used;
    
    public List<List<Integer>> permute(int[] nums) {
        used = new boolean[nums.length];
        traversal(nums);
        return ans;
    }

    public void traversal(int[] nums) {
      // 遍历到叶子节点的时候说明结束了，而叶子节点的判断就是是不是  
      if (path.size() >= nums.length) {
            ans.add(new ArrayList<>(path));
            return;
        }
        for(int i = 0; i < nums.length; i++) {
          // 如果使用过直接先跳过  
          if (used[i] == true) {
                continue;
            }
            used[i] = true;
            path.add(nums[i]);
            traversal(nums);
          // 回溯的过程
            used[i] = false;
            path.remove(path.size() - 1);
        }
    }
}
```

