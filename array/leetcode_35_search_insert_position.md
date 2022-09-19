### Question 35 Search Insert Position

![image-20220626192140269](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220626192140269.png)

又是一道经典的二分查找题目，为什么是二分查找呢？其实只需要看几个关键信息。这道题目要求时间复杂度为O(log n)，并且给了一个排好序的数组

不论是什么样的二分查找，其实涉及到的就是一些边界的判断，比如说是应该left<right, left <= right, left = mid + 1, left = mid ??? 这里一般采用的原则有两个，一个是左闭右开，一个是左闭右闭。我个人比较喜好左闭右开，所以代码也是根据这个原则写的。



```java
class Solution {
    public int searchInsert(int[] nums, int target) {
        int left = 0, right = nums.length; // 左闭右开，所以right所代表的下标不应该包含在数组里
        // 若是left <= right，就打破了right下标不应该在数组里的原则
        while (left < right) {
            int mid = (left + right) / 2;
            if (nums[mid] > target) {
                right = mid;
            } else if (nums[mid] < target) {
                left = mid + 1; // 看到跟right的不同了吧，因为左边是闭，left所代表的下标应该在数组里可以被找到
            } else {
                return mid;
            }
        }
        return right;
    }
}
```

