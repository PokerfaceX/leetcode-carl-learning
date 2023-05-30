### Question 90 Subsets II

![image-20230514161502026](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230514161502026.png)

这道题目其实是一个leetcode_40和leetcode_78的混合题目，再一次涉及到了树层的去重。去重的逻辑和第40题一摸一样，这里就不在重复了。添加的逻辑也和leetcode_78一样，每一个节点都是一个答案，添加到ans中，也不需要任何剪枝操作，因为每一个树枝都是需要的

```java
class Solution {

    List<Integer> path = new ArrayList<>();
    List<List<Integer>> ans = new ArrayList<>();

    public List<List<Integer>> subsetsWithDup(int[] nums) {
        Arrays.sort(nums);
        backtracking(nums, 0);
        return ans;
    }

    public void backtracking(int[] nums, int startIndex) {
        ans.add(new ArrayList<>(path));
        for(int i = startIndex; i < nums.length; i++) {
            if (i != startIndex && nums[i] == nums[i - 1]) {
                continue;
            }
            path.add(nums[i]);
            backtracking(nums, i + 1);
            path.remove(path.size() - 1);
        }

    }


}
```

