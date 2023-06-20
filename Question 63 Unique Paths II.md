### Question 63 Unique Paths II

![image-20230619235506428](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230619235506428.png)

- dp数值的含义
  - 从(0, 0)到达坐标(i ,j)的路径数量, 就是dp[i] [j]，如果有障碍物，就是0，因为无法抵达
- 递推公式
  - dp[i] [j] = dp[i - 1] [j] + dp[i] [j - 1]，如果这俩其中一个有障碍物，因为到达有障碍物的点的路径数量为0，所以也无所谓，不影响结果
  - 稍微注意的一点就是，当目前的点有障碍物的时候，我们就不使用递推公式了，直接跳过
- 初始化
  - 第一排，第一列，全部初始成1，但是要注意的是，如果碰到障碍物，后面的也得变成0
  - 遍历整个二位数值，如果有障碍物，弄成0
- 遍历顺序
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

