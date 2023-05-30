### Question 47 Permutations II

![image-20221125202733748](/Users/jasonjin/Library/Application Support/typora-user-images/image-20221125202733748.png)



~~~java
class Solution {
    
    List<Integer> path = new ArrayList<>();
    List<List<Integer>> ans = new ArrayList<>();
    boolean[] used;
    
    public List<List<Integer>> permuteUnique(int[] nums) {
        used = new boolean[nums.length];
        Arrays.sort(nums);
        traversal(nums);
        return ans;
    }

    public void traversal(int[] nums) {
        if (path.size() >= nums.length) {
            ans.add(new ArrayList<>(path));
            return;
        }
        for(int i = 0; i < nums.length; i++) {
          // 去重的逻辑，树层去重，used[i - 1] == false就是树层去重，因为会被回溯
            if (i > 0 && nums[i] == nums[i - 1] && used[i - 1] == false) {
                continue;
            }
          // 逻辑的话和46类似，用来跳过当前已经加入到path里的数字
            if (used[i] == true) {
                continue;
            }
            used[i] = true;
            path.add(nums[i]);
            traversal(nums);
            used[i] = false;
            path.remove(path.size() - 1);
            
            
        }
    }
}
~~~

