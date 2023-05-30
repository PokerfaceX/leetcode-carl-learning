### Question 45 Jump Game II

![image-20230521172324203](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230521172324203.png)

这道题目，其实答案很难想到，我们需要两个两个变量，一个用来统计当前的遍历范围，一个记录下一个最大的范围

![image-20230521172441778](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230521172441778.png)

上代码来解释

```java
class Solution {
    public int jump(int[] nums) {
        int currCover = 0, nextCover = 0;
        int result = 0;
        for(int i = 0; i < nums.length; i++) {
          // 在遍历当前最大范围时，找到下一个最大范围，记录下来
            nextCover = Math.max(nextCover, i + nums[i]);
            if (i == currCover) {
              // 当i走到了当前的最大范围的时候，如果是数组最后面直接break然后返回就行了
                if (i == nums.length - 1) {
                    break;
                } else {
                  // 如果走到了当前的最大范围但是还没有到最后一个位置，就说明我们要进入下一个范围，那么就要递增result，并且让currCover更新一下
                    result++;
                    currCover = nextCover;
                }
            }
        }
        return result;
    }
}
```

