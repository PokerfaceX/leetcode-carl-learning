### Question 844 Backspace String Compare

![image-20230415152112644](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230415152112644.png)

这道题目就用stack就可以做出来，没啥逻辑，碰到#就删除，不然就加进去

```python
class Solution:
    def backspaceCompare(self, s: str, t: str) -> bool:
        def getActualText(s: str) -> list:
            stack = []
            for c in s:
                if c == '#':
                    if len(stack) == 0:
                        continue
                    else:
                        stack.pop()
                else:
                    stack.append(c)
            return stack
        return getActualText(s) == getActualText(t) # python通过 == 可以直接对比list的数值和顺序
            

```



上面 我试着用了python的嵌套方法，在一个方法里面来定义另外一个方法，然后对于这种情况，不用传入self参数，只有当这个方法是一个实例方法的时候，第一个参数必须得是self，这是python语法定义的