### Question 93 Restore IP Addresses

![image-20221111215401093](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20221111215401093.png)

这道题目算得上是有难度的一道题目，必须得先搞懂leetcode_131。

![image-20221111215502514](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20221111215502514.png)

我们每一次分割，都会看当前分割的字符串是不是合法的，如果是，那就继续向下递归，如果不是，那就直接中断循环。

```java
class Solution {

    List<String> ans = new ArrayList<>();

    public List<String> restoreIpAddresses(String s) {
        traversal(s, 0, 0);
        return ans;
    }
	
    // 这里得用numOfDots来标记叶子节点
    public void traversal(String s, int startIndex, int numOfDots) {
        // 这里稍微有点特殊，总共是四段字符串，那么就需要有三个句号
        if (numOfDots == 3) {
            // 当有三个句号的时候就得把startIndex之后的字符全部加上
            if (isValidString(s, startIndex, s.length() - 1)) {
                ans.add(new String(s));
            }
            return;
        }
        for(int i = startIndex; i < s.length(); i++) {
            if (isValidString(s, startIndex, i)) {
                // 这里直接加上句号方便之后添加进ans
                s = s.substring(0, i + 1) + "." + s.substring(i + 1);
                numOfDots++;
                // 这里有个细节就是递归的时候因为加了个句号所以得从i + 2开始
                traversal(s, i + 2, numOfDots);
                // 回溯的过程
                numOfDots--;
                // 注意这里是吧之前的句号给去掉
                s = s.substring(0, i + 1) + s.substring(i + 2);
            }
        }

    }
	
    // 判断是不是一个合适的ip地址的元素
    public boolean isValidString(String s, int startIndex, int endIndex) {
        // 当startIndex遍历到最后的时候，如果不加上下面这个判断就会报错
        if (startIndex > endIndex) {
            return false;
        }
        // 清除那些以0开头的非法的ip地址
        if (s.charAt(startIndex) == '0' && startIndex != endIndex) {
            return false;
        }
        // 从字符串构造数字，看看是不是在[0, 255]
        int number = 0;
        for(int i = startIndex; i <= endIndex; i++) {
            number *= 10;
            number += s.charAt(i) - '0';
        }
        return number <= 255;
    }
}
```

