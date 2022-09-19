### Question 485 Max Consecutive Ones

![image-20220630142016995](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220630142016995.png)

第一次看这道题目的时候想到了用滑动窗口，想了下如何移动窗口，也想了很多边角情况。其实代码比想象的简单很多，简单来说，用一个指针遍历数组，只要碰到1，就开始个内循环，看看连续的数字1有几个。



```java
class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {
        int i = 0;
        int length = Integer.MIN_VALUE;
        while (i < nums.length) {
            if (nums[i] == 1) {
                int j = i;
                while (j < nums.length && nums[j] == 1) {
                    j++;
                }
                length = Math.max(length, j - i);
                i = j;
            }
            i++;
        }
        return length == Integer.MIN_VALUE ? 0 : length;
    }
}
```



注意，虽然用了两个while循环但是时间复杂度还是O(N)，原因的话就是整个数组的每个数值，只是遍历了一遍。