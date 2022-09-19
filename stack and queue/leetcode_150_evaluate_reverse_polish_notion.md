### Question 150 Evaluate Reverse Polish Notation

![image-20220916210934313](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220916210934313.png)

这道题目比较简单明了，用一个栈存放一下数字，再用一个栈存放一下操作符，每当遇到操作符的时候，就从数字栈里面pop两个数值，进行运算，再把最新数值加到栈里面。

上代码

```java
class Solution {
    public int evalRPN(String[] tokens) {
        Stack<String> operators = new Stack<>();
        Stack<Integer> numbers = new Stack<>();
        
        for(String s: tokens) {
            if (s.equals("+")) {
                int val1 = numbers.pop();
                int val2 = numbers.pop();
                numbers.add(val1 + val2);
            } else if(s.equals("-")) {
                int val1 = numbers.pop();
                int val2 = numbers.pop();
                numbers.add(val2 - val1); // 注意下这里应该是val2 - val1，看看图就理解了
            }  else if(s.equals("*")) {
                int val1 = numbers.pop();
                int val2 = numbers.pop();
                numbers.add(val1 * val2);
            } else if (s.equals("/")) {
                int val1 = numbers.pop();
                int val2 = numbers.pop();
                numbers.add(val2 / val1);
            } else {
                numbers.add(Integer.valueOf(s));
            }
        }
        
        return numbers.pop();
    }
}
```

