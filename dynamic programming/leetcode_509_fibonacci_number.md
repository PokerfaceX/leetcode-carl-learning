### Question 509 Fibonacci Number

![image-20230605230007562](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230605230007562.png)

- dp数组的含义？

dp[n]就表示在一个fibonacci series里面第n个数字的具体数值

- dp公式

dp[n] = dp[n - 1] + dp[n - 2]

- dp遍历顺序

从左到右就好了

- dp的初始值

第一个初始为0，第二个初始为1，其余无所谓，遍历的时候在计算就行了

dp模拟

- 脑海里模拟了一遍感觉ok



```java
class Solution {
    public int fib(int n) {
      // edge case处理
        if (n == 1 || n == 0) {
            return n;
        }
        int[] dp = new int[n + 1];
        dp[0] = 0;
        dp[1] = 1;
        for(int i = 2; i < n + 1; i++) {
            dp[i] = dp[i - 1]+ dp[i - 2];
        }
        return dp[n];
    }
}
```

