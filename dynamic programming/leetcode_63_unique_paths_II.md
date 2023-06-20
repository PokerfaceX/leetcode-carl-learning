### Question 63 Unique Paths II

![image-20230620215024713](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230620215024713.png)

dp含义

- 从(0, 0)到(i, j)总共有多少条路径呢？dp[i] [j]

递推公式

- dp[i] [j] = max(dp[i - 1] [j], dp[i] [j - 1])
- 如果当前有障碍物，就为0

初始化

- 第一排，第一列，在障碍物之前全部初始化为1，障碍物以及障碍物之后变成0

遍历顺序

- 从左到右，从上到下



```java
class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        int m = obstacleGrid.length;
        int n = obstacleGrid[0].length;
        int[][] dp = new int[m][n];
        for(int i = 0; i < m; i++) {
            if (obstacleGrid[i][0] == 1) {
               break;
            }
            dp[i][0] = 1;
       }
       for(int j = 0; j < n; j++) {
           if (obstacleGrid[0][j] == 1) {
               break;
           }
           dp[0][j] = 1;
       }
        for(int i = 1; i < m; i++) {
            for(int j = 1; j < n; j++) {
                if (obstacleGrid[i][j] == 1){
                    continue;
                }
                dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
            }
        }
        System.out.println(Arrays.deepToString(dp));
        return dp[m - 1][n - 1];
    }
}
```

