### Question 134 Gas Station

![image-20230522224912935](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230522224912935.png)

有难度的一道贪心算法，这里的话直接上代码解释

```java
class Solution {
    public int canCompleteCircuit(int[] gas, int[] cost) {
        int start = 0;
        int currSum = 0, totalSum = 0;
      // 如果总共要消耗的汽油是多余能补充的汽油的，那么神仙来了都不可能绕一圈
        for(int i = 0; i < gas.length; i++) {
            totalSum += gas[i] - cost[i];
        }
        if (totalSum < 0) {
            return -1;
        }
      // 不用考虑循环，因为如果i是不合法的起点，我们就不用去管他，因为最终我们想要的合法起点只有1个
        for(int i = 0; i < gas.length; i++) {
            currSum += gas[i] - cost[i];
            if (currSum < 0) {
              // 这里是最难理解的一步，看下面的解释
                start = i + 1;
                currSum = 0;
            }
        }
        return start;
    }
}
```

假设，我们从节点i开始走，走到了节点k，这时候发现，油(currSum)不够了，走不到，那么我们寻找的起点只能在k之后，为什么呢，因为我们知道，合法的起点只有1个，假设i+1是一个合法的起点，那么i+1这个节点就永远不会碰到currSum为负数的情况，而且已经假设了节点i不是一个合法的starting point，所以只需要向后遍历

同理，当我们到节点k的时候，我们会发现，节点k之前的节点全部都没有满足过让currSum < 0的情况，所以直接让start = k+1就好了，逻辑有点绕，其实用的是数学的思想

![image-20230522225816878](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230522225816878.png)