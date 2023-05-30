### Question 78 Subsets

![image-20230514155919274](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230514155919274.png)

这道题目也是一道回溯算法能解决的经典问题，但是比较特殊，因为在这里我们不会在叶子节点收集结果。

![image-20230514160026431](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230514160026431.png)

在每一个节点，我们都应该把当前的子集加入到最终结果中，而不是单单的遍历到叶子节点在进行收集的操作。

```java
class Solution {
    List<Integer> path = new ArrayList<>();
    List<List<Integer>> ans = new ArrayList<>();

    public List<List<Integer>> subsets(int[] nums) {
        traversal(nums, 0);
        return ans;
    }

    public void traversal(int[] nums, int startIndex) {
        // 收集结果的语句我们放到了第一行，不是if判断之后，因为放在if之后的话，在每一个叶子节点的时候，startIndex都是大于nums.length的，那么叶子节点的子集就不会被加入到ans中。
        ans.add(new ArrayList<>(path));
        // 这个判断其实也是可写可不写，就算不写，for循环也会自己终止，而且是不需要任何剪枝的，我们要找到所有节点
        if (startIndex >= nums.length) {
            return;
        }
        for(int i = startIndex; i < nums.length; i++) {
            path.add(nums[i]);
            traversal(nums,i + 1);
            path.remove(path.size() - 1);        
        }
    }
}
```

