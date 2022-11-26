### Question 47 Permutations II

![image-20221125202733748](/Users/jasonjin/Library/Application Support/typora-user-images/image-20221125202733748.png)

其实这道题目和前面所有的去重题目都很类似，都需要用到used数组与排序。之所以要排序是因为要和他前面的元素进行对比来查看是否已一样，used数组可以来查重。



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
            if (i > 0 && nums[i] == nums[i - 1] && used[i - 1] == false) {
                continue;
            }
          // 下面的这一步就是导致一开始错误的原因，如果没有这一行，那么我就没法判断一个元素到底有没有加入过数组里，比如说当前数组为[1, 1, 2]，我在第一层for循环加入了一个1，那么因为我没有startIndex，我还是从i == 0开始遍历，我很容易把同一个下标的元素重复使用。
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

