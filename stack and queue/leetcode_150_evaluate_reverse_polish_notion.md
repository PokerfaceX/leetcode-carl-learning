### Question 150 Evaluate Reverse Polish Notation

![image-20230502234213862](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230502234213862.png)

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



这里的话考虑了一下代码设计的问题，做了一点点代码重构，但是没有使用两个栈

```java
class Solution {
    public int evalRPN(String[] tokens) {
        Stack<String> stack = new Stack<>();
        for(String s: tokens) {
            if (s.equals("+")) {
                int[] nums = this.getTwoValuesFromStack(stack);
                stack.add(nums[0] + nums[1] + "");
            } else if (s.equals("-")) {
                int[] nums = this.getTwoValuesFromStack(stack);
                stack.add(nums[1] - nums[0] + "");
            } else if (s.equals("*")) {
                int[] nums = this.getTwoValuesFromStack(stack);
                stack.add((nums[0] * nums[1]) + "");
            } else if (s.equals("/")) {
                 int[] nums = this.getTwoValuesFromStack(stack);
                 stack.add((nums[1] / nums[0]) + "");
            } else {
                stack.add(s);
            }
        }
        return Integer.valueOf(stack.pop());
    }

    public int[] getTwoValuesFromStack(Stack<String> stack) {
        int num1 = Integer.valueOf(stack.pop());
        int num2 = Integer.valueOf(stack.pop());
        return new int[]{num1, num2};
    }
}
```

