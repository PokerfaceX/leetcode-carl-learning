### Question 40 Combination Sum II

![image-20221106085352320](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20221106085352320.png)

这道题目的关键在于去重，在最终的答案里，不能出现相同的组合

举个例子[1, 1, 2], target = 3，在这里我们只能返回一个[1, 2]

但是要注意的是，尽管不能有重复的答案，且每一个数字在组合中只能使用一次，但是这每一个数字是针对candidates数组里面的下标而言的。意思就是说同一个index对应的数字只能使用一次，所以第一个1和第二个1实际上指的是不同的数字.

这道题目，卡哥给了两个关键词，树层去重和树枝去重，看图

![image-20221106085729516](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20221106085729516.png)

~~~java
class Solution {
    
    List<Integer> path = new ArrayList<>();
    List<List<Integer>> ans = new ArrayList<>();
    boolean[] used;
    
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        
        Arrays.sort(candidates);
        this.used = new boolean[candidates.length];
        traversal(candidates, target, 0, 0);
        return ans;
    }

    public void traversal(int[] candidates, int target, int currSum, int startIndex) {
        if (currSum > target) {
            return;
        }
        if (currSum == target) {
            ans.add(new ArrayList<>(path));
            return;
        }
        for(int i = startIndex; i < candidates.length; i++) {
            // 这里如果是used[i - 1] == true，那么就会抛弃所有类似于[1, 1]的情况，这不是我们想要的，我们想要删除的只是回溯过程结束之后发现前面有重复的数值才跳过 
            if (i > 0 && used[i - 1] == false && candidates[i] == candidates[i - 1]) {
                continue;
            }
            path.add(candidates[i]);
            used[i] = true;
            traversal(candidates, target, currSum + candidates[i], i + 1);
            path.remove(path.size() - 1);
            used[i] = false;
        }
    }
}
~~~

