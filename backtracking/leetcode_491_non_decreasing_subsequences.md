### Question 491 Non-decreasin Subsequences

![image-20230514230645679](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230514230645679.png)

这道题目和之间回溯算法里面做过的去重不太一样(leetcode_40)，和子序列也不太一样(leetcode_90)，这里的话因为是要从当前的数列中找到所有递增的子序列，所以不能排序，所以去重的方法也不一样



![image-20230514230845968](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230514230845968.png)

上代码

```java
class Solution {

    List<Integer> path = new ArrayList<>();
    List<List<Integer>> ans = new ArrayList<>();

    public List<List<Integer>> findSubsequences(int[] nums) {
        traversal(nums, 0);
        return ans;
    }

    public void traversal(int[] nums, int startIndex) {
      // 我们需要收集所有尺寸大于1的子节点，所以不能加return语句  
      if (path.size() > 1) {
            ans.add(new ArrayList<>(path));
        }
      // 用来记录当前这一层的数值有没有被用过
        Set<Integer> set = new HashSet<>();
        for(int i = startIndex; i < nums.length; i++) {
            // 如果当前的数值小于path的最后一位数，那就是非法的了
            if (!path.isEmpty() && nums[i] < path.get(path.size() - 1)) {
                continue;
            }
          // 如果已经在set里面了，就说明当前层所有包含nums[i]的情况已经被收集过了
          // 用了两个if语句，看起来更好理解，而且set不用回溯，因为每一层都是一个新的variable就可以了
            if (set.contains(nums[i])) {
                continue;
            }
            path.add(nums[i]);
            set.add(nums[i]);
            traversal(nums, i + 1);
            path.remove(path.size() - 1);
        }
    }
}
```

