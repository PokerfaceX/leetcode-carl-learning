### Question 26 Remove Duplicates from Sorted Array

![image-20220627212410714](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220627212410714.png)

![image-20220627212422429](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220627212422429.png)

其实这道题目，一开始想的时候可能会有点懵，但是其实就是一道经典的滑动窗口题目。滑动窗口的入门请参考一下文章，

[leetcode_209_长度最小的子数组]: https://mp.csdn.net/mp_blog/creation/success/125471531



其实大概的逻辑就是，当fast指针所遍历到的数值与slow数值所指向的数值不同的时候，我们就让slow指针所指向的下一个数值等于当前fast的数值。

代码如下：

```java
class Solution {
    public int removeDuplicates(int[] nums) {
        int slow = 0, fast = 0;
        while (fast < nums.length) {
            if (nums[slow] != nums[fast]) {
                nums[++slow] = nums[fast];
            } 
            fast++;
        }
        return ++slow;
    }
}
```

简单解释下nums[++slow] = nums[fast]，在这里slow的数值会先加一，在被赋值成nums[fast]。