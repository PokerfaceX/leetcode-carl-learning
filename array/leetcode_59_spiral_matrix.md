### Question 59 Spiral Matrix II

![image-20230322221642140](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230322221642140.png)

虽然这道题目的难度是medium，但是本身的逻辑比较简单。拿以上n=3的情况来说，只需要在外围一圈逐次添加数值，中心位置单独赋值就可以了。

废话不多说了，上代码

```java
class Solution {
    // 假设这里n==3
    public int[][] generateMatrix(int n) {
        int[][] array = new int[n][n];
        int numOfLoops = n / 2; // 大家可以画个图理解下为什么是n/2
        int i = 0, number = 1, offset = 1;
        while (i < numOfLoops) {
            int row = i;
            int column = i;
            //这里是负责y=0 -> y = 1
            while (column < n - offset) {
                array[row][column++] = number++;  
            }
            // 这里是负责x == 0 -> x == 1
            while (row < n - offset) {
                array[row++][column] = number++;
            }
            // 这里是负责y == 2 -> y == 1
            while (column > i) {
                array[row][column--] = number++;
            }
            // 这里是负责x == 2 -> x == 1
            while (row > i) {
                array[row--][column] = number++;
            }
            offset++;
            i++;
        }
        // 若是n为奇数，则再进行一次额外的赋值，给数组的正中央赋值
        if (n % 2 != 0) {
            array[n/2][n/2] = number;
        }
        return array;
    }
}
```

可以看到代码不难理解，但是可能会有一些关于offset的疑问。可以看到在上面的四次while循环中，没有直接循环到边界的情况，都是跟边距有一点距离的，而这个距离就是offset。有了offset，才好进行赋值，否则则需要一大堆if语句，极其容易使代码变得混乱。



```python
class Solution:
    def generateMatrix(self, n: int) -> List[List[int]]:
        nums = [[0] * n for _ in range(n)]
        count = 1
        startX, startY = 0, 0
        loop, mid = n // 2, n // 2
        for offset in range(1, loop + 1):
            for i in range(startY, n - offset):
                nums[startX][i] = count
                count += 1
            for i in range(startX, n - offset):
                nums[i][n - offset] = count
                count += 1
            for i in range(n - offset, startY, -1):
                nums[n - offset][i] = count
                count += 1
            for i in range(n - offset, startX, -1):
                nums[i][startY] = count
                count += 1
            startX += 1
            startY += 1
        if n % 2 != 0:
            nums[mid][mid] = count
        return nums
```

