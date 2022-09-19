### Question 18 4Sum

![image-20220910111748734](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220910111748734.png)

这道题目和15题三数之和非常的像，逻辑基本是相同的，但是多了一点点去重和剪枝的细节。



例子[-2, -2, 0, 0]， target == -4

上代码

```java
class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target) {
        List<List<Integer>> ans = new ArrayList<>();
        Arrays.sort(nums);
        for(int i = 0; i < nums.length; i++) {
            // 注意这里，我们需要加一个nums[i] > 0，拿上面例子来说如果-2 > -4， 不写这个判断直接就会被跳过，当nums[i] > 0且大于target的时候，是可以continue的，因为后面的数值加上去肯定是越来越多，不会越来越小
            if (nums[i] > target && nums[i] > 0) {
                return ans;
            }
            if (i > 0 && nums[i] == nums[i - 1]) {
                continue;
            }
            for(int j = i + 1; j < nums.length; j++) {
				// 如果数组是[2,2,2,2], target == 8，我们不写j > i + 1就会跳过一个题解，但是我们仍然需要做一个查重的操作，所以只要j不是在和i做对比，且出现了重复的j，我们就跳过去
                if (j > i + 1 && nums[j] == nums[j - 1]) {
                    continue;
                }
                
                int left = j + 1;
                int right = nums.length - 1;
                while (left < right) {
                    if (nums[i] + nums[j] + nums[left] + nums[right] > target) {
                        right--;
                    } else if (nums[i] + nums[j] + nums[left] + nums[right] < target) {
                        left++;
                    } else {
                        ans.add(Arrays.asList(nums[i], nums[j], nums[left], nums[right]));
                        while(left < right && nums[left] == nums[left + 1]) left++;
                        while(left < right && nums[right] == nums[right - 1]) right--;
                        left++;
                        right--;
                    }
                }
            }
            
            
        }
        return ans;
    }
}
```

