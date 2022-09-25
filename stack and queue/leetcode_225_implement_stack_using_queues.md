### Question 225 Implement Stack Using Queues

![image-20220915144220955](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220915144220955.png)

这道题目的话，本身思路不难，但是代码随想录上面java的题解非常不好，所以耽误了很多时间。假设一个stack的数值为 [1,2,3,4   那么根据题目，我们需要两个queue。Queue1用来储存stack的所有数值，所以queue1为[1,2,3,4]，然后当我们需要pop的时候，把1，2，3放到queue2，这时候queue2就是[1,2,3]，queue1只剩下一个"4"，我们把4给pop掉，再把queue2的所有数值加回到queue1

~~~java
class MyStack {
    
    Queue<Integer> queue1 = new LinkedList<>();
    Queue<Integer> queue2 = new LinkedList<>(); // 辅助队列
    
    public MyStack() {
        
    }
    
    public void push(int x) {
        queue1.add(x);
    }
    
    public int pop() {
        while (queue1.size() > 1) {
            queue2.add(queue1.poll());
        }
        int value = queue1.poll(); // 这时候queue1只有一个数值，所以pop掉
        // 把queue2的数值加回到queue1
        while(queue2.size() > 0) {
            queue1.add(queue2.poll());
        }
        return value;
    }
    
    public int top() {
        while (queue1.size() > 1) {
            queue2.add(queue1.poll());
        }
        // 注意，这时候queue1确实只剩下了一个数值，也是我们想要的
        int value = queue1.poll(); // 这里如果使用了peek，数值就会留在queue1中，我们在从queue2加回到queue1就会出现bug
        // 加回去
        while(queue2.size() > 0) {
            queue1.add(queue2.poll());
        }
        // 我们是直接把top的数值给pop掉了，这样在加回去的时候顺序是对的，然后在把top的数值加回到queue1就好
        queue1.add(value);
        return value;
    }
    
    public boolean empty() {
        return queue1.isEmpty();
    }
~~~



上面的方法虽然麻烦，但是逻辑是非常清晰的

下面就是一个queue来实现，假设stack是1，2，3，4]，那么queue还是[1，2，3，4]，在我们想pop的时候，我们只需要把queue的前三个数字再放到后面去[4，1，2，3]

```java
class MyStack {
    
    Deque<Integer> queue;
    
    public MyStack() {
        queue = new LinkedList<>();
    }
    
    public void push(int x) {
        queue.addLast(x);
    }
    
    public int pop() {
        int size = queue.size();
        while (size > 1) {
            queue.addLast(queue.poll());
            size--;
        }
        return queue.poll();
    }
    // 其实从原理上讲，也应该像是上面一样把前面的东西全部放到后面，但是因为麻烦就直接peekLast了
    public int top() {
        return queue.peekLast();
    }
    
    public boolean empty() {
        return queue.isEmpty();
    }
}

/**
 * Your MyStack object will be instantiated and called as such:
 * MyStack obj = new MyStack();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.top();
 * boolean param_4 = obj.empty();
 */
```

