### Question 435 Non-overlapping Intervals

![image-20230527222023871](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230527222023871.png)

<img src="/Users/jasonjin/Library/Application Support/typora-user-images/image-20230527223005345.png" alt="image-20230527223005345" style="zoom:50%;" />

这道题目和leetcode_452非常非常相似，做这道题也是再次加深了对leetcode_452的理解，这里直接上代码解释

这道题目贪心就贪心在，我们只要找到每一个overlap的区间，并且把他们统计出来，就是要移除的区间数量，并不需要真的删除array里面的元素

```java
class Solution {
    public int eraseOverlapIntervals(int[][] intervals) {
        Arrays.sort(intervals, (a, b) -> a[0] - b[0]);
        int count = 0;
        for(int i = 1; i < intervals.length; i++) {
          // 如果当前左边界大于等于之前的右边界，那我们就啥都不干，跳过就好
            if (intervals[i][0] >= intervals[i - 1][1]) {
                continue;
            } else {
              // 如果在边界的话，就说明我们找到了一个要移除的区间，把它的右边界更新一下，用来找到overlap的点，以此来和下一个区间做对比
                count++;
                intervals[i][1] = Math.min(intervals[i][1], intervals[i - 1][1]);
            }
        }
        return count;
    }
}
```

