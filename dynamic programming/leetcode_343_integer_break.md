### Question 343 Integer Break

![image-20230620214331397](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230620214331397.png)

dp数组的含义

- dp[i]代表着一个数字i，被拆分之后，可以得到的最大乘积

递归公式

- dp[i] = max(j * (i - j), j * dp[i - j], dp[i])
- 这里稍微解释下这个公式，当我们想计算最大乘积的时候，肯定被拆分成至少x1和x2，那么x2，我们是拆分还是不拆分呢？答案是，无法确定，看x=5的情况，这里可以被拆分成2 * 3，那么我们后面的3，要不要继续拆分呢？这个就得看上面的公式了2 * 3和2 * dp[3]哪个大？dp[3]是2，所以这里就小于普通的2*3了
- 后面的dp[i]是因为我们用的两层for循环，dp[i]的数值需要不断的被比较才能知道

初始化

- dp[1], dp[0]这俩数值没法被拆分，所以全部初始化成0，让他不被影响

遍历顺序

- 从左到右



```java
class Solution {
    public int integerBreak(int n) {
        int[] dp = new int[n + 1];
        dp[0] = 0;
        dp[1] = 0;
        dp[2] = 1;
        for(int i = 3; i <= n; i++) {
            for(int j = 1; j < i; j++) {
                dp[i] = Math.max(Math.max(j * (i - j), j * dp[i - j]), dp[i]);
            }
        }
        return dp[n];
    }
}
```

