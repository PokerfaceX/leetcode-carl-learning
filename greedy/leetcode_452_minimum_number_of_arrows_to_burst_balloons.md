### Question 452 Minimum Number of Arrows to Burst Balloons

![image-20230527160323789](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230527160323789.png)

又是一道非常难想到解法的题目，这里我直接看卡哥的图片

![image-20230527160413648](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230527160413648.png)

其实贪心的原理就是，让每一个弓箭，尽可能的射穿多个气球，那么这样的局部最优，就会导致全局最优，而且我想不出明显的反例

```java
class Solution {
    public int findMinArrowShots(int[][] points) {
        // 根据气球直径的开始坐标从小到大排序
        // 使用Integer内置比较方法，不会溢出
        Arrays.sort(points, (a, b) -> Integer.compare(a[0], b[0]));
        int count = 1;  // points 不为空至少需要一支箭
        for (int i = 1; i < points.length; i++) {
            if (points[i][0] > points[i - 1][1]) {  // 气球i和气球i-1不挨着，注意这里不是>=
                count++; // 需要一支箭
            } else {  // 气球i和气球i-1挨着
                points[i][1] = Math.min(points[i][1], points[i - 1][1]); // 更新重叠气球最小右边界
            }
        }
        return count;
    }
}
```