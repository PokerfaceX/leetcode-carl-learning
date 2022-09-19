### Question 349 Intersection of Two Arrays

![image-20220908223846743](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220908223846743.png)

这道题目的逻辑本身并不复杂， 定义一个set来存放nums1的数值，若是nums2的任意数值在set里面出现过，就说明是交集

**这里特地解释一下，hashmap的搜索的时间复杂度是O(1)，原因是因为hashmap的底层原理是数组加上链表或者红黑树，当数组里的元素过多的时候，数组的每一个单位就会从链表形式切换到红黑树的形式，更多的原理就去看https://blog.csdn.net/v123411739/article/details/115364158?spm=1001.2014.3001.5502**

上代码

```java
class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        Set<Integer> set1 = new HashSet<>();
        for(int i = 0; i < nums1.length; i++) {
            set1.add(nums1[i]);
        }
        Set<Integer> ans = new HashSet<>();
        for(int i: nums2) {
            if (set1.contains(i)) {
                ans.add(i);
            }
        }
        // 最后一行的话，就是把set切换成流，在换成int流，int流的每一个数值由i.intValue()组成再换成数组
        return ans.stream().mapToInt(i -> i.intValue()).toArray();
    }
}
```

