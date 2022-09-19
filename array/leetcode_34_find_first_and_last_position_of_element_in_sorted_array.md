### Question 34 Find First and Last Position of Element in Sorted Array

![image-20220626201728967](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220626201728967.png)

若是完全理解这道题目就说明完全理解了二分查找！

一开始直接看给的条件

- [x] 给了排序好的数组

- [x] 找某个数值
- [x] 时间复杂度为O(log n)

这三个条件全部满足，很显然需要用到二分查找。



然而， 这道题目难就难在一些边界的判定和对于二分查找的一些修改。



如第一个例子，再找target == 8的时候，需要分别找到两个下标，那么我们就需要对寻常的二分查找代码进行一些更改了。



```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int start = search(nums, target, true);
        int end = search(nums, target, false);
        
        return new int[]{start, end};
    }
    
    public int search(int[] nums, int target, boolean leftBiased) {
        // 这里leftBiased代表的就是我们是不是要找最左侧的target，反之就是找最右侧的target
        int left = 0, right = nums.length; 
        int result = -1; // 用来看到最后有没有找到数值
        // 左闭右开
        while (left < right) {
            int mid = (left + right) / 2;
            if (nums[mid] > target) {
                right = mid; // 标准写法
            } else if (nums[mid] < target) {
                left = mid + 1; // 标准写法
            } else {
                result = mid;
                if (leftBiased) {
                    right = mid; // 因为找最左侧的target所以我们在让right=mid且继续往左侧查找
                } else {
                    left = mid + 1; // 继续往右侧查找
                }
                
            }
        }
        return result;
    }
    
    
}
```



这里顺便加一下左闭右闭的写法，这两个的区别我在另一篇文章里写过. 

[]: https://blog.csdn.net/jasonjin1107/article/details/125443796	""leetcode第704题""



```java
public int search(int[] nums, int target, boolean leftBiased) {
        int left = 0, right = nums.length - 1; 
        int result = -1;
        while (left <= right) {
            int mid = (left + right) / 2;
            if (nums[mid] > target) {
                right = mid - 1;
            } else if (nums[mid] < target) {
                left = mid + 1; 
            } else {
                result = mid;
                if (leftBiased) {
                    right = mid - 1;
                } else {
                    left = mid + 1;
                }
                
            }
        }
        return result;
    }
```

