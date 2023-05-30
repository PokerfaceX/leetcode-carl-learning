### Question 1047 Remove All Adjacent Duplicates In String

![image-20230503214514926](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230503214514926.png)

比较简单的一道题目，只需要用一个栈，每当push进一个字符的时候，就看看栈顶上面的字符，如果相等，就pop，不相等，就加入到栈中
~~~java
class Solution {
    public String removeDuplicates(String s) {
        Stack<Character> stack = new Stack<>();
        for(char c: s.toCharArray()) {
            if (!stack.isEmpty() && stack.peek() == c) {
                stack.pop();
            } else {
                stack.add(c);
            }
        }
        StringBuffer a = new StringBuffer();
        // 这里其实是正向遍历的stack，如果调用pop那就是相反的sh
        for(char c: stack) {
            a.append(c);
        }
        return a.toString();
    }
}
~~~

上面的代码其实就是最基本的题解，但是为了优化一下代码，其实我们可以使用StringBuffer来模拟一个栈

```java
class Solution {
    public String removeDuplicates(String s) {
        Stack<Character> stack = new Stack<>();
        for(char c: s.toCharArray()) {
            if (stack.isEmpty()) {
                stack.add(c);
            } else {
                char topLetter = stack.peek();
                if (topLetter == c) {
                    stack.pop();
                } else {
                    stack.push(c);
                }
            }
        }
        StringBuilder sb = new StringBuilder();
        for(char c: stack) {
            sb.append(c);
        }
        return sb.toString();
    }
}
```





