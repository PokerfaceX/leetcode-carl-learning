### Question 151 Reverse Words in a String

![image-20220911200123100](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220911200123100.png)

这道题目可以注意到的细节是，前后的空格需要移除，而且单词之间的空格可能有好几个，我们只能保存一个。

思路的话其实蛮直接的，直接反转整个字符串，在分别反转一个个单词就好

```java
class Solution {
    public String reverseWords(String s) {
        StringBuffer sb = removeExtraSpace(s);
        reverse(sb, 0, sb.length() - 1);
        reverseWord(sb);
        return sb.toString();
    }
    
    public StringBuffer removeExtraSpace(String s) {
        int i = 0, j = s.length() - 1;
        StringBuffer sb = new StringBuffer();
        while(i < s.length() && s.charAt(i) == ' ') i++; // 移除前面的空格
        while(j >= 0 && s.charAt(j) == ' ') j--; // 移除后面的空格
        while (i <= j) {
            // 如果不是空格，就直接加进sb，如果是空格的话，就看sb当前的最后一个字符是什么，以免加入重复的空格
            if (s.charAt(i) != ' ' || sb.charAt(sb.length() - 1) != ' ') {
                sb.append(s.charAt(i));
            }
            i++;
        }
        return sb;
    }
    
    // reverse the string between start and end
    public void reverse(StringBuffer sb, int start, int end) {
        while (start <= end) {
            char c = sb.charAt(start);
            sb.setCharAt(start, sb.charAt(end));
            sb.setCharAt(end, c);
            start++;
            end--;
        }
    }
    
    public void reverseWord(StringBuffer sb) {
        int start = 0;
        int end = 0;
        while (start < sb.length()) {
            // 找到
            while(end < sb.length() && sb.charAt(end) != ' ') end++;
            reverse(sb, start, end - 1);
            start = end + 1;
            end = start;
        }
    }
}
```

