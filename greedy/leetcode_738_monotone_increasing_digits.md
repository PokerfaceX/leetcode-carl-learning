### Question 738 Monotone Increasing Digits

![image-20230530192709535](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230530192709535.png)

解题思路？

- 非常的巧妙，拿332举例子，第二个3大于2，那么我们应该让这个3自减，然后把2变成9

原因？

- 因为我们需要选择小于332并且尽量大的数字，不可能减小2，因为这样不会是递增的



```java
class Solution {
    public int monotoneIncreasingDigits(int n) {
        char[] array = Integer.valueOf(n).toString().toCharArray();
      // 这里的flag是干嘛的？举个例子，1000，我们如果对比后直接赋值9，那么就会是"0900"，这不是我们想要的，我们需要记录一个下标，让下标和之后的所有数字都为9
      // 为什么要记录成这么array.length，因为如果是0或者-1的话后面的for循环会错误的把所有数字变成9
        int flag = array.length;
        for(int i = array.length - 2; i >= 0; i--) {
            if (array[i] > array[i + 1]) {
                array[i]--;
                flag = i + 1;
            }
        }
        for(int i = flag; i < array.length; i++) {
            array[i] = '9';
        }
        return Integer.parseInt(String.valueOf(array));
    }
}
```

这道题目只能从后往前遍历吗？

- 没错，因为从后往前遍历我们是知道哪些数字变成了9的，而且当前的遍历是基于前面的计算，向前遍历达不到这种效果

为什么要赋值成9？

- 因为数值要越大越好