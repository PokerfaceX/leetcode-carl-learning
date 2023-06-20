### Question 62 Unique Paths

![image-20230618142715164](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230618142715164.png)

dp数组的含义

- ```dp[i][j]``` ：表示从（0 ，0）出发，到(i, j) 有多少条不同的路径。

状态转移公式

- ```dp[i][j] = dp[i - 1][j] + dp[i][j - 1]```，因为这里机器人只能往下面或者右边走，到达一个点的路径总和就是左侧和上方的路径数量全部加起来

初始化

- 第一横排全部定义为1，因为确实只有一直往右走这么一条路径
- 第一竖排全部定义为1，因为确实只有一直往下走这么一条选项

遍历顺序

- 从左到右一层层遍历
- 第一个竖排和横排都不用管



```java
class Solution {
    public int uniquePaths(int m, int n) {
        int[][] dp = new int[m][n];
        for(int i = 0; i < m; i++) {
            for(int j = 0; j < n; j++) {
                if (i == 0 || j == 0) {
                    dp[i][j] = 1;
                }
            }
        }
        for(int i = 1; i < m; i++) {
            for(int j = 1; j < n; j++) {
                dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
            }
        }
        return dp[m - 1][n - 1];
    }
}
```

