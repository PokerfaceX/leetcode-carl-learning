### Question 20 Valid Parentheses

![image-20220915153654426](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220915153654426.png)

这道题目的思路倒是蛮简单的，我们把左侧括号全部放进栈中，在看右侧括号和栈中pop出来的左侧括号匹不匹配，就能知道是不是一个valid parenthesis

~~~java
class Solution {
    public boolean isValid(String s) {
        Stack<Character> stack = new Stack<>();
        for(char c: s.toCharArray()) {
            if (c == '(' || c == '{' || c == '[') {
                stack.add(c);
            } else {
                if (stack.isEmpty()) {
                    return false;
                }
                char c2 = stack.pop();
                if (c2 == '(' && c == ')') {
                    continue;
                } else if (c2 == '[' && c == ']') {
                    continue;
                } else if (c2 == '{' && c == '}') {
                    continue;
                } else {
                    return false;
                }
            }
        }
        return stack.isEmpty(); //不能直接写false，因为有些时候可能是"[()"，循环里面匹配没毛病但是stack有剩余说明还是没有匹配成功
    }
}
~~~



上面的代码其实有点冗余，所以稍微修正下思路，让代码变得简洁一点
~~~java
class Solution {
    public boolean isValid(String s) {
        Stack<Character> stack = new Stack<>();
        for(char c: s.toCharArray()) {
            if (c == '(') {
                stack.add(')');
            } else if (c == '[') {
                stack.add(']'); // 大佬的想法， 直接往栈里面放入正解，这样的话栈顶代表的就是应该匹配的右侧括号
            } else if (c == '{') {
                stack.add('}');
            } else {
                // 栈为空或者当前字符和栈顶的期望括号不相同就说明错了
                if (stack.isEmpty() || stack.pop() != c) {
                    return false;
                }
            }
            
        }
        return stack.isEmpty();// yi'yang'de
    }
}
~~~

