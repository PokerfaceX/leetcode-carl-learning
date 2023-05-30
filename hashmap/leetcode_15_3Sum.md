### Question 15 3Sum

![image-20230429231511674](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230429231511674.png)

这道题目，看了题解，才理解做法。其实本质上就是双指针，但是这道题目，难就难在去重上。举个例子，如果数组是[-1, -1, -1, 1, 1, 2]，那么我们只能返回一个答案也就是[-1, -1, 2]，如果没有好好去重，那么就有可能导致出现重复的答案。

上代码

```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> ans = new ArrayList<>();
        // 数组如果没有被排序，那么就无法使用双指针
        Arrays.sort(nums);
        for(int i = 0; i < nums.length; i++) {
            // 第一个数字已经是正数了，那么后面就不可能有解
            if (nums[i] > 0) {
                return ans;
            }
            /*
            	这里解决的其实就是i的重复问题，还是数组[-1, -1, -1, 1, 1, 2], 那么当i等于第一个-1
            	的时候，其实我们就已经找到了所有以-1开始的triplet，所以我们可以跳过所有i为-1的情况
            */
            /*
            	这里有一个需要注意的点，就是nums[i] == nums[i + 1]这样的写法是行不通的，因为这会导致我				  们的triplet永远没有重复的数值，还是以数组[-1, -1, -1, 1, 1, 2]为例子，我们将永远无法				  找到答案为[-1, -1, 2]的triplet
            */
            if (i > 0 && nums[i] == nums[i - 1]) {
                continue;
            }
            int left = i + 1;
            int right = nums.length - 1;
            while (left < right) {
                if (nums[i] + nums[left] + nums[right] > 0) {
                    right--;
                } else if (nums[i] + nums[left] + nums[right] < 0) {
                    left++;
                } else {
                    ans.add(Arrays.asList(nums[i], nums[left], nums[right]));
                    //同理，我们找到了所有nums[i]为某个数字，nums[left]为某个数值的情况，所以当nums[left]出现重复的时候，直接跳过就好
                    while(left < right && nums[left] == nums[left + 1]) left++;
                    while(left < right && nums[right] == nums[right - 1]) right--;
                    //上面的两个while循环如果没有重复数值出现就不会启动，所以还是要进行j
                    left++;
                    right--;
                }
            }
        }
        return ans;
    }
}
```

 ```python
 class Solution:
     def threeSum(self, nums: List[int]) -> List[List[int]]:
         ans = list()
         nums.sort()
         for curr in range(len(nums)):
             if nums[curr] > 0:
                 return ans
             if curr > 0 and nums[curr] == nums[curr - 1]:
                 continue
             left, right = curr + 1, len(nums) - 1
             while left < right:
                 total = nums[curr] + nums[left] + nums[right]
                 if total > 0:
                     right -= 1
                 elif total < 0:
                     left += 1
                 else:
                     ans.append([nums[curr], nums[left], nums[right]])
                     while left < right and nums[left] == nums[left + 1]: left += 1
                     while left < right and nums[right] == nums[right - 1]: right -= 1
                     left += 1
                     right -= 1
         return ans
 ```

