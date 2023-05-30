### Question 376 Wiggle Subsequence

![image-20230520202901022](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230520202901022.png)

这是一道贪心的题目， 为什么呢？看下面这个图，在下面的图中，只要我们删掉这些“不合适”的数字，就能得到最大的wiggle sequence，当然这里面我们只需要统计长度，不用真的删除数值

而且还有一个有趣的知识点，subsequence：A **subsequence** is obtained by deleting some elements (possibly zero) from the original sequence, leaving the remaining elements in their original order.

![image-20230520203050369](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230520203050369.png)



这道题目代码简单，但是其实真的挺难的，有多种情况要考虑，我们需要时刻知道前面的diff是多少，后面的diff是多少，好看到当前这个数是不是一个wiggle sequence

![image-20230520203031555](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230520203031555.png)

### 情况2:

如何处理第一个数字的preDiff和最后一个数字的currDiff



![image-20230520203306206](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230520203306206.png)

上代码解释

```java
class Solution {
    public int wiggleMaxLength(int[] nums) {
        int preDiff = 0;
      // 处理情况2，我们不必遍历到最后一个数字，直接把最后一个数字当成一个峰值才处理
        int result = 1;
      // 同理，不遍历到最后一个数值
        for(int i = 0; i < nums.length - 1; i++) {
          // 看下一个数字和当前数字的差距，得到currDiff
            int currDiff = nums[i + 1] - nums[i];
          // 这里preDiff == 0才是卡哥的神来之笔，这样就能解决情况1，脑海里面模拟一下就知道了，对于这种例子[1,2,2,3]在遍历第二个2的时候才会检测到坡度的变化
            if ((preDiff >= 0 && currDiff < 0) || (preDiff <= 0 && currDiff > 0)) {
                result++;
              // 把这个assign statement放在这里用来处理情况3[1,2,2,2,3,4]，因为第三个2不是一个合法的坡度变化的点，所以我们的想法就是，preDiff只用来记录，之前坡度变化时候的数值
                preDiff = currDiff;
            }
        }
        return result;
    }
}
```

这道题目是看的卡哥b站的讲解，很推荐看
