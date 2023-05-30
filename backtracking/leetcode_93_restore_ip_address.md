### Question 93 Restore IP Addresses

![image-20230514144514910](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230514144514910.png)

这道题目算得上是有难度的一道题目，必须得先搞懂leetcode_131。

![image-20230514144533927](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230514144533927.png)

我们每一次分割，都会看当前分割的字符串是不是合法的，如果是，那就继续向下递归，如果不是，那就直接中断循环。

```java
class Solution {

    int numOfDots = 0;
    List<String> ans = new ArrayList<>();
    StringBuffer sb = new StringBuffer();


    public List<String> restoreIpAddresses(String s) {
        this.sb = new StringBuffer(s);
        backtracking(sb, 0);
        return ans;
    }

    public void backtracking(StringBuffer sb, int startIndex) {
      // 当有三个点的时候，就说明现在已经是一个我们在测试的ip地址了，已经有了四段数值，所以直接检查是不是一个合法的ip字符串，从startIndex开始到最后面一个字符进行检查
        if (this.numOfDots == 3) {
            if (isValidIp(sb.substring(startIndex, sb.length()))) {
                ans.add(sb.toString());
                return;
            }
        }
        for(int i = startIndex; i < sb.length(); i++) {
            if (isValidIp(sb.substring(startIndex, i + 1))) {
                // 因为知道从[startIndex, i]是一个合法ip地址，就往i+1前面插入一个“.”
                sb.insert(i + 1, ".");
                this.numOfDots++;
                backtracking(sb, i + 2);
              // 回溯操作
                sb.deleteCharAt(i + 1);
                this.numOfDots--;
            }
        }
    }
		
    public boolean isValidIp(String string) {
      // 有些时候进行检查的有可能是一个空的字符串比如"111.22.22."，我们没有传进来一段字符串，这时候直接返回false  
      if (string.isBlank()) {
            return false;
        }
      // 任何以0开头且长度大于1的肯定也是错的
        if (string.charAt(0) == '0' && string.length() > 1) {
            return false;
        }
      // 如果长度大于3，怎么着都是false的
        if (string.length() > 3) {
            return false;
        }
        int num = Integer.valueOf(string);
        return num <= 255;
    }
}
```

