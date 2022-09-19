### Question 283 Move Zeroes

![image-20220628154314206](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220628154314206.png)

又是一道经典的滑动窗口题目，具体的知识点可以参考我之前的这篇帖子

[leetcode26_删除重复项]: https://blog.csdn.net/jasonjin1107/article/details/125488372

废话不多说，直接上代码

```java
class Solution {
    public void moveZeroes(int[] nums) {
        int slow = 0, fast = 0;
        while (fast < nums.length) {
            if (nums[fast] != 0) {
                nums[slow++] = nums[fast];
            }
            fast++;
        }
        //非0的数值已经都被放到了前面，后面的数值得按照题目要求变成0
        while(slow < nums.length) {
            nums[slow++] = 0;
        }
        return;
    }
}
```

