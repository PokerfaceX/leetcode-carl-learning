### Question 209 Minimum size Subarray Sum

leetcode题目209

以下是题目介绍

![image-20230416081138443](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230416081138443.png)

这道题目是一道滑动窗口的经典问题，这里滑动窗口的原则就是为了让窗口里的数值符合条件，也就是大于等于target，当满足条件的时候便从左侧开始逐渐减少窗口的长度(用来找出最短窗口长度)，直到滑动窗口里的数值不满足题目条件为止



```java
class Solution {
    public int minSubArrayLen(int target, int[] nums) {
        int slow = 0, fast = 0;
        int currentSum = 0;
        int length = Integer.MAX_VALUE;
        while (fast < nums.length) {
            currentSum += nums[fast];
            // 之所以是>=而不是>的原因就是只要窗口里的数值满足题目条件就应该计算一次长度
            while (currentSum >= target) {
                length = Math.min(length, fast - slow + 1);
                currentSum -= nums[slow++];
            }
            fast++;
        }
        System.out.println("fast is " + fast + " slow is " + slow);
        return length == Integer.MAX_VALUE ? 0: length ;
    }
}
```





```python
class Solution:
    def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        left, right = 0, 0
        currSum = 0
        length = sys.maxsize
        for right in range(len(nums)):
            currSum += nums[right]
            while currSum >= target:
                length = min(right - left + 1, length)
                currSum -= nums[left]
                left += 1
        return 0 if length == sys.maxsize else length
```







