### Question 70 Climbing Stairs

![image-20230606225257161](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230606225257161.png)

1. 确定dp数组，以及下标的的含义 - dp数组代表着抵达阶梯n有多少种方法
2. 确定递归公式， dp[n] = dp[n - 1] + dp[n - 2]
3. 确定遍历顺序，从左到右
4. 确定初始值，dp[0]这里直接抛弃，dp[1] = 1, dp[2] = 2

```java
class Solution {
    public int climbStairs(int n) {
        if (n == 1 || n == 2) {
            return n;
        }
        int[] dp = new int[n + 1];
      // 这里dp[0]没有意义因为不存在楼层0这个东西
        dp[1] = 1;
        dp[2] = 2;
        for(int i = 3; i < n + 1; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }
        return dp[n];
    }
}
```

