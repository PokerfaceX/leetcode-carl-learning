### Question 90 Subsets II

![image-20221112140131631](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20221112140131631.png)

这道题目其实是一个leetcode_40和leetcode_78的混合题目，再一次涉及到了树层的去重。

![image-20221112140250028](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20221112140250028.png)

```java
class Solution {
    List<Integer> path = new ArrayList<>();
    List<List<Integer>> ans = new ArrayList<>();
    boolean[] used;
    
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        used = new boolean[nums.length];
        Arrays.sort(nums);
        traversal(nums, 0);
        return ans;
    }

    public void traversal(int[] nums, int startIndex) {
        ans.add(new ArrayList<>(path));
        if (startIndex > nums.length) {
            return;
        }
        for(int i = startIndex; i < nums.length; i++) {
            // 这里之所以看是不是false是因为我们要做的是树层去重，当回溯过后used[i - 1]肯定是false，那么这个时候如果当前数值和前一个数值相等，就肯定是重复得了
            if (i != 0 && nums[i] == nums[i - 1] && used[i - 1] == false) {
                continue;
            }
            path.add(nums[i]);
            used[i] = true;
            traversal(nums, i + 1);
            used[i] = false;
            path.remove(path.size() - 1);
        }
    }
}
```

