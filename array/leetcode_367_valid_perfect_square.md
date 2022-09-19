### Question 367 Valid Perfect Square

![image-20220627205833905](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220627205833905.png)

这道题目和我之前发布过的https://blog.csdn.net/jasonjin1107/article/details/125487064?csdn_share_tail=%7B%22type%22%3A%22blog%22%2C%22rType%22%3A%22article%22%2C%22rId%22%3A%22125487064%22%2C%22source%22%3A%22jasonjin1107%22%7D&ctrtid=qfpyk很相似，都是涉及到了二分查找.

而唯一的不同是，我这里直接把left，right以及mid都用long来表达。这样的话就不用担心溢出的问题，别的不多说了，直接上代码。有任何疑问可以观看我之前写过的关于二分查找的帖子



```java
class Solution {
    public boolean isPerfectSquare(int num) {
        long left = 1, right = num + 1;
        while (left < right) {
            long mid = (left + right) / 2;
            // 不可以写 mid > num / mid的形式，因为会自动转换成整数，举个例子，在计算机中，5 == 29/5，su
            if (mid * mid > num) {
                right = mid;
            } else if (mid * mid < num) {
                left = mid + 1;
            } else {
                return true;
            }
        }
        return num == 1 ? true: false;
    }
}
```

