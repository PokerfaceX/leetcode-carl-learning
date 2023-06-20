### Question 746 Min Cost Climbing Stairs

![image-20230617225741788](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230617225741788.png)

确定dp数组，以及下标的的含义

- dp数组代表着，到达当前这个index，最小的花费是什么

确定递归公式

- array[currIndex] = Min(array[currIndex - 2] + cost[currIndex - 2] , array[currIndex - 1] + cost[currIndex - 1])

- 我从当前位置，不管是跳一步还是两步，都需要把当前的cost加上

确定遍历顺序

- 从左到右

确定初始值

- dp[0] = 0, dp[1] = 0，因为我们的数组代表着到达这个index所需要的最小花费，我们是可以从index0或者index1开始的，到达这两个初始坐标并不需要任何花费，但是从这两个位置出发，往上跳，就需要花费了
- 然后注意一下，dp的数组得多一个格子，因为还有一个“顶层”



```java
class Solution {
    public int minCostClimbingStairs(int[] cost) {
        int[] dp = new int[cost.length + 1]; // 一个顶层，代表着到达顶层的时候最小花费是多少
        dp[0] = 0;
        dp[1] = 0;
        for(int i = 2; i < dp.length; i++) {
            dp[i] = Math.min(dp[i - 1] + cost[i - 1], dp[i - 2] + cost[i - 2]);
        }
        return dp[dp.length - 1];
    }
}
```

