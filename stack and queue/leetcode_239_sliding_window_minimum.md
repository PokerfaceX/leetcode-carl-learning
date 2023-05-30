### Question 239 Sliding Window Minimum

![image-20230503212117109](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230503212117109.png)

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



代码随想录的题解讲的不怎么好，这里看的neetcode的题解

https://www.youtube.com/watch?v=DfljaUwZsOk&t=152s



```java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        // 这个就相当于是我们灵活的队列，最前面的数值就是当前窗框的最大值
        Deque<Integer> deque = new LinkedList<>();
        int left = 0, right = 0;
        int index = 0;
        int[] array = new int[nums.length - k + 1]; // 储存答案
        while(right < nums.length) {
          	// 每次我们想加入数值的时候，从队列的最后面一个个看，如果要加入的数值大于栈的最右侧数值，就一个个移除，甚至可以全部移除，也就是说要加入的数值大于之前窗口里面所有的数值
            while (!deque.isEmpty() && nums[deque.getLast()] < nums[right]) {
                deque.removeLast();
            }
          // 这里我们储存的是下标，方便到时候移除不在当前窗口的数值
            deque.addLast(right);
          	// 如果left下标大于我们队列的最左侧（最大值）的下标，就说明这个数字不属于当前窗口，移除它
            if (left > deque.getFirst()) {
                deque.removeFirst();
            }
          // 很难想到的情况，如果right下标小于k的话说明我们连第一个窗口都没看完
            if (right + 1 >= k) {
                // left下标也应该不断的迭代，
                array[index++] = nums[deque.getFirst()];
                left++;
            }
            right++;
        }
        return array;

        
    }
}
```

