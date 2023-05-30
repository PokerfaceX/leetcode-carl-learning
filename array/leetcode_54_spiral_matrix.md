### Question 54 Spiral Matrix

![image-20230322215649176](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230322215649176.png)

这一道题目，提示思路题目里面已经告诉你了，就是从外到内以螺旋的方式一层一层的打印出数值。而我这里的思路是，分别定义四个边界，top, bottom, left, right，在一个while循环中加上四个内循环，分别从top left 打印到top right, top right打印到bottom right, bottom right到bottom left，再从bottom left到top left。每当我们打印完一行或者一列之后需要调整边界。

上代码

```java
class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        int top = 0, left = 0, right = matrix[0].length - 1, bottom = matrix.length - 1; 
        List<Integer> ans = new ArrayList<>();
        while (top <= bottom && left <= right) {
            //top left to top right
            for(int i = left; i <= right; i++) {
                ans.add(matrix[top][i]);
            }
            top++;
            
            // top right to bottom right
            for(int i = top; i <= bottom; i++) {
                ans.add(matrix[i][right]);
            }
            right--;
            //这一步的话可以调试来理解，再有些情况下，比如第二个例子，会涉及到多次打印重复位置的情况。
            if (!(left <= right && top <= bottom)) {
                break;
            }
            // bottom right to bottom left
            for(int i = right; i >= left; i--) {
                ans.add(matrix[bottom][i]);
            }
            bottom--;
            
            // bottom left to top left
            for(int i = bottom; i >= top; i--) {
                ans.add(matrix[i][left]);
            }
            left++;
        }
        return ans;
        
    }
}
```



```python3
class Solution:
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
        left, right = 0, len(matrix[0])
        top, bottom = 0, len(matrix)
        ans = []
        while left < right and top < bottom:
            # top left -> top right
            for i in range(left, right):
                ans.append(matrix[top][i])
            top += 1
            # top right -> bottom right
            for i in range(top, bottom):
                ans.append(matrix[i][right - 1])
            right -= 1
            if not (left < right and top < bottom):
                break
            # bottom right -> bottom left 
            for i in range(right - 1, left - 1, -1):
                ans.append(matrix[bottom - 1][i])
            bottom -= 1
            # bottom left -> top left
            for i in range(bottom - 1, top - 1, -1):
                ans.append(matrix[i][left])
            left += 1
        return ans
```



