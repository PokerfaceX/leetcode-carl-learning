### Question 239 Sliding Window Minimum

![image-20220916230653630](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220916230653630.png)

对于这道题目而言，如果能有这么一个Queue，可以用O(1)的方法获得当前窗口的最大数值，那么就会让整个答案变成O(n)，因为我们唯一需要做的就是，遍历nums这个数组，poll一下，add一下，在找一下最大值，只要能让这三个操作变成O(1)，那么就会是最优化的题解，其实可以发现这个队列是一个单调队列，也就是说这个队列里面的数值永远是递增或者递减的

上代码解释

```java
// 自己定义一个queue
class MyQueue {
        Deque<Integer> queue;
        
        public MyQueue() {
            this.queue = new LinkedList<>();
        }
        // 当新加入的数值大于queue的末尾数值的时候，一直移除数值
        public void add(int x) {
            while (!queue.isEmpty() && queue.getLast() < x) {
                queue.removeLast();
            }
            queue.addLast(x);
        }
        // 当想要pop的数值等于最大数值的时候，才会从queue里面移除
        public void poll(int x) {
            if (!queue.isEmpty() && queue.getFirst() == x) {
                queue.removeFirst();
            }
        }
        // 返回queue里面最前面的数值，同时也是最大值
        public int getMax() {
            return queue.getFirst();
        }
    }

class Solution {
    
    
    public int[] maxSlidingWindow(int[] nums, int k) {
        MyQueue queue = new MyQueue();
        int[] ans = new int[nums.length - k + 1]; // 用来存放所有窗口的最大值
        int j = 0;
        
        for(int i = 0; i < k; i++) {
            queue.add(nums[i]); // 把前面k数值加进去，因为我们的队列大小最多为K
        }
        ans[j++] = queue.getMax();
        int left = 0, right = k;
        while (right < nums.length) {
            queue.poll(nums[left]);
            queue.add(nums[right]);
            ans[j++] = queue.getMax();
            left++;
            right++;
        }
        return ans;
    }
}
```

https://programmercarl.com/0239.%E6%BB%91%E5%8A%A8%E7%AA%97%E5%8F%A3%E6%9C%80%E5%A4%A7%E5%80%BC.html

可能到时候会有点懵，点击网站上面的bilibili链接，画一下就会很好理解