### Question 347 Top K Frequent Elements

![image-20220919095250255](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220919095250255.png)

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



更多关于堆的原理解析： https://juejin.cn/post/6893744125486006285