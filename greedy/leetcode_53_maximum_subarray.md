### Question 53 Maximum Subarray

![image-20230520211554558](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230520211554558.png)

这道题目也要用到贪心算法，只是有点难想到，其实关键的思路就是，当连续和负数的时候，我们马上摒弃这个连续和，直接使用当前的数值。之所以这样是因为，哪怕下一个数值是负数，只要连续和为负数，加上下一个数字后，只会让负数更负。



```java
class Solution {
    public int maxSubArray(int[] nums) {
        int result = 0;
        int ans = Integer.MIN_VALUE;
        for(int i = 0; i < nums.length; i++) {
          // 如果连续和result为负数，直接采取当前数值
            if (result < 0) {
                result = nums[i];
            } else {
              // 如果连续和为正数，加上当前数字，怎么着都会比当前数字大，所以直接加上去
                result = result + nums[i];
            }
          // 每次都有做比较，因为最大的连续自数组之和可以随时被发现
            ans = Math.max(result, ans);
        }
        return ans;
    }
}
```

这道题目，一个非常重要的概念就是，不是找到负数就摒弃连续子数和，而是**连续子数和**为负数的时候才摒弃

下面的解释我觉得很有用

![image-20230520212201244](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230520212201244.png)