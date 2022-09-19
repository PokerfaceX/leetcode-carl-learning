### Question 69 Sqrt(x)

![image-20220627202928414](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220627202928414.png)

这道题目，用到的是二叉查找的思想。原因就是，在二分查找的过程中，若是找到了平方根，那么直接返回就可以，若是没有，在二分查找的循环结束之后，left或者right的数值就是最接近题目要求的数值(这里就不进行数学的证明了，反正试一下就知道了)。



```java
class Solution {
    public int mySqrt(int x) {
        // 因为没写下面这个判断，错了很多次
        if (x == 0 || x == 1) {
            return x;
        }
        int left = 1, right = x;
        while (left < right) {
            int mid = (left + right) / 2;
            if (mid > x / mid) {
                right = mid;
            } else if (mid  < x / mid) {
                left = mid + 1;
            } else {
                return mid;
            }
        }
        return right - 1;
    }
}
```



这里可能会对mid > x / mid, mid < x / mid这样的语句有疑问。为什么不写成mid * mid > x或者mid * mid<x这种更好理解的方式。这是因为会涉及到溢出的问题，举个例子，int的最大数值约为21亿，也是题目里给的x最大数值，那么此时，mid的数值约为10个亿。大家想象一下，十亿的平方该有多大？肯定是大于int的最大值的，程序就会溢出，可能就会出现未知错误。 