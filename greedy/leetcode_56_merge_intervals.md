### Question 56 Merge Intervals

![image-20230529233306343](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230529233306343.png)

这道题目的话和前面的弓箭射气球，和non_overlapping_interval都非常相似，都是跟找区间有关的问题

这里直接上代码解释

```java
class Solution {
    public int[][] merge(int[][] intervals) {
        Arrays.sort(intervals, (a, b) -> a[0] - b[0]);
        List<List<Integer>> ans = new ArrayList<>();
        ans.add(Arrays.asList(intervals[0][0], intervals[0][1]));
        for(int i = 1; i < intervals.length; i++) {
          // 如果当前左边界小于上一个右边界，那么说明有重合
            List<Integer> prevList = ans.get(ans.size() - 1);
            if (intervals[i][0] <= prevList.get(1)) {
              // 看这种例子[[1,9], [2, 7]]很明显可以合并成一个区间，但是右边界具体取哪个就要看max了
                prevList.set(1, Math.max(intervals[i][1], prevList.get(1)));
            } else {
              // 像这种情况[[1,2], [4,5]]很明显就是两个区间
                ans.add(Arrays.asList(intervals[i][0], intervals[i][1]));
            }
        }
      //只有list<int[]>才可以直接调用toArray方法
        return ans.stream().map(list -> new int[]{list.get(0), list.get(1)}).toArray(int[][]::new);
    }
}
```

