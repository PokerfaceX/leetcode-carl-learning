### Question 232 Implement Queue using Stacks

![image-20220914231856188](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220914231856188.png)

对于这道题目而言，用一个stack储存输入的数值，一个stack用来储存要输出的数值，才能解决问题。假设一个queue是1->2->3->4，那么stack in就是[1,2,3,4]，这时候我们想pop一下，那么我们就需要把stack in的数值全部导入到stack out，那么stack out就是[4,3,2,1]，stack in为[]，所以直接从stack out里面pop，得出我们想要的1这个数值

```java
class MyQueue {
    
    Stack<Integer> inStack = new Stack<>();
    Stack<Integer> outStack = new Stack<>();
    
    public MyQueue() {
        
    }
    
    public void push(int x) {
        inStack.add(x);
    }
    
    public int pop() {
        if (outStack.isEmpty()) {
            while (!inStack.isEmpty()) {
                outStack.add(inStack.pop());
            }
        }
        return outStack.pop();
    }
    
    public int peek() {
        if (outStack.isEmpty()) {
            while (!inStack.isEmpty()) {
                outStack.add(inStack.pop());
            }
        }
        return outStack.peek();
    }
    
    public boolean empty() {
        return inStack.isEmpty() && outStack.isEmpty();
    }
    
}

/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue obj = new MyQueue();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.peek();
 * boolean param_4 = obj.empty();
 */
```



上面可以看到，从instack导入到outstack的操作进行了一次重复，为了解决这个code smell，分出一个function

```java
class MyQueue {
    
    Stack<Integer> inStack = new Stack<>();
    Stack<Integer> outStack = new Stack<>();
    
    public MyQueue() {
        
    }
    
    public void push(int x) {
        inStack.add(x);
    }
    
    public int pop() {
        dumpFromInStack();
        return outStack.pop();
    }
    
    public int peek() {
        dumpFromInStack();
        return outStack.peek();
    }
    
    public boolean empty() {
        return inStack.isEmpty() && outStack.isEmpty();
    }
    
    // helper function
    public void dumpFromInStack() {
        if (outStack.isEmpty()) {
            while (!inStack.isEmpty()) {
                outStack.add(inStack.pop());
            }
        }
    }
    
}

/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue obj = new MyQueue();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.peek();
 * boolean param_4 = obj.empty();
 */
```

