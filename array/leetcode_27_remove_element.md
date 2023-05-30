### Question 27 Remove Element

![image-20230320221230535](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230320221230535.png)

![image-20230320221246359](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230320221246359.png)

#####  

这道题目是快慢指针的经典应用，也叫双指针法

大概逻辑如下：

定义一个指针为fast，一个指针为slow，fast指针快速遍历整个数组并且找出不等于val(要删除的数值)的值，把他赋值给slow指针的引用。

一开始写的代码如下:

```java
class Solution {
    public int removeElement(int[] nums, int val) {
        int slow = 0, fast = 0;
        int newLength = 0;
        while (fast < nums.length) {
            while (fast < nums.length && nums[fast] == val) {
                fast++;
            } 
            if (fast < nums.length) {
                nums[slow++] = nums[fast++];
                newLength++;
            }
            
        }
        return newLength;
    }
}
```

写完这样的方法之后不太满意，觉得条件判断语句重复了好多次，观看了下大佬们的解法。



```java
class Solution {
    public int removeElement(int[] nums, int val) {
        int slow = 0, fast = 0;
        int newLength = 0;
        while (fast < nums.length) {
            // 神来之笔，若是fast指针不同于val，那么直接赋值给slow指针的引用即可，但是fast指针是每一次循环都需要递增，要不然会导致无限循环
            if (nums[fast] != val) {
                nums[slow++] = nums[fast];
                newLength++;
            }
            fast++;
            
        }
        return newLength;
    }
}
```



```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        slow, fast = 0, 0
        while fast < len(nums):
            if nums[fast] != val:
                nums[slow] = nums[fast]
                slow += 1
            fast += 1
        return slow
```

