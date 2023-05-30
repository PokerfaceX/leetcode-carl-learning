### Question 347 Top K Frequent Elements

![image-20230503212136953](/Users/jasonjin/Library/Application Support/typora-user-images/image-20230503212136953.png)

这道题目其实是一道Priority Queue的经典应用，Priority Queue的底层本是一个堆的数据结构，他的add, remove等操作都是O(log(n))，对于这道题目，我们可以先使用map来统计每一个元素出现的次数，再把它们加到priority queue来实现自动的排序，那么最高时间复杂度就是O(n * log(n))。



```java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        PriorityQueue<int[]> pQueue = new PriorityQueue<>((pair1, pair2) -> pair2[1] - pair1[1]); // 这里的话用过lambda表达式来实现了一个comparator接口
        Map<Integer, Integer> map = new HashMap<>();
        for(int i: nums) {
            map.put(i, map.getOrDefault(i, 0) + 1);
        }
        for(Integer i: map.keySet()) {
            pQueue.add(new int[]{i, map.get(i)});
        }
        int[] ans = new int[k];
        for(int i = 0; i < k; i++) {
            ans[i] = pQueue.poll()[0];
        }
        return ans;
    }
}
```



更多关于堆的原理解析： https://juejin.cn/post/6893744125486006285和https://www.youtube.com/

这里的话更新一下做法， 思路一样，但是更加优雅

```java
class Solution {
  /*Comparator接口说明:
 * 返回负数，形参中第一个参数排在前面；返回正数，形参中第二个参数排在前面
 * 对于队列：排在前面意味着往队头靠
 * 对于堆（使用PriorityQueue实现）：从队头到队尾按从小到大排就是最小堆（小顶堆），
 *                                从队头到队尾按从大到小排就是最大堆（大顶堆）--->队头元素相当于堆的根节点
 * */
    public int[] topKFrequent(int[] nums, int k) {
        PriorityQueue<int[]> priorityQueue = new PriorityQueue<>((pair1, pair2) -> {
          // 实现大顶堆实现，哪一个数字出现的次数多，哪一个就在前面，之所以是pair2[1] - pair1[1]是因为comparator接口的原因，阅读下上面的说明就好
          return pair2[1] - pair1[1];
        });
        Map<Integer, Integer> map = new HashMap<>();
        for(Integer integer: nums) {
            map.put(integer, map.getOrDefault(integer, 0) + 1);
        }
        for(Map.Entry<Integer, Integer> entry: map.entrySet()) {
            priorityQueue.add(new int[]{entry.getKey(), entry.getValue()});
        }
        int[] ans = new int[k];
        for(int i = 0; i < k; i++) {
            ans[i] = priorityQueue.poll()[0];
        }
        return ans;

    }
}
```

