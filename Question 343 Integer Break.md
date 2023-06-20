### Question 343 Integer Break

![image-20230620213219575](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230620213219575.png)

dp数值的含义

- dp[i]代表着拆分i之后可以得到的最大乘积

递推公式

- dp[i] = max(j * i - j, j * dp[i - j], dp[i])
- 这里需要稍微解释下上面的代码，一个数字比如说**x**但他被拆分的时候，肯定可以被拆分成两个数字，那么这时候难道直接取，假设拆封成**x1, x2**难道dp[x1] * dp[x2]一定就是最大的吗？答案是，不一定。比如说5，最大乘积其实就是2 * 3，dp[3]这里是2(1 * 2)，所以就不应该拆分后面那个3了，直接取x1和x2的乘积就行了
- 所以上面的递推公式，实际上计算得是，我们该不该拆分数值，而最后的dp[i]其实就是因为我们这里是个for循环所以要不停的和之前得到的数值进行比较
- 为什么j不用分解呢？其实有点点绕，但是仔细一想，当你之前计算dp[j]的时候，其实已经把j的所有拆分情况试过了，因为j是从1开始的，可以看下面的第二个for循环

初始化

- 这里就没啥可说的了，dp[0]和dp[1]全部变成0就好了，因为他们没法被拆分

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

